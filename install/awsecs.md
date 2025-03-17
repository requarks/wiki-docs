---
title: AWS ECS
description: Getting started with a Wiki.js installation on AWS ECS
published: true
date: 2023-09-01T02:32:37.749Z
tags: 
editor: markdown
dateCreated: 2023-05-25T22:35:20.633Z
---

> This guide was contributed by the community and may be incomplete or become outdated.
{.is-warning}

# Overview

This guide details the step-by-step procedure to deploy Wiki.js on AWS using their managed service offerings. 
We'll use Elastic Container Service to run the container and the Relational Database Service for the PostgreSQL database. 

Alternatively, you could bundle run it all on a single EC2 instance but that is essentially already covered in the Linux installation guide.

By the end of this, we'll deploy
- An ECS cluster running the WikiJS container
- An Amazon RDS for Postgres instance
- An Application Load Balancer

# Prerequisites

1. An AWS account
1. Existing VPC with at least two subnets
1. An EC2 instance to run PostgreSQL client.

# Security Groups

We will need two security groups, one for the load balancer and another for the database.
Navigate to the EC2 service, and select **Security Groups**.

## Database Security Group

1. Click **Create Security Group**
1. Complete the form
	- Security group name: **wikijs-database**
	- Click **Add Rule** under Inbound rules
  	- Type: **PostgreSQL**
    - Source: **Custom** and your VPC CIDR (e.g. 10.0.0.0/24)
    - Description: **PostgreSQL access for WikiJS**
1. Click **Create Security Group**

## Load Balancer Security Group

1. Click **Create Security Group**
1. Complete the form
	- Security group name: **wikijs-elb**
	- Click **Add Rule** under Inbound rules
  	- Type: **HTTP**
    - Source: **Anywhere-IPv4**
    - Description: **HTTP to wiki**
1. Click **Create Security Group**

# IAM Role

Navigate to the **IAM** service, then under **Roles** 

1. Click **Create Role**.
	- Trusted entity type: **AWS Service**
	- Use case: **Elastic Container Service**, then **Elastic Container Service Task**
	- Click **Next**
1. Add permissions
	- AmazonSSMReadOnlyAccess
	- AmazonECSTaskExecutionRolePolicy
  - Click **Next**

1. Role name: **WikijsTaskExecutionRole**
1. Click **Create Role**

# Parameters

We're going to store our database password in Systems Manager Parameter Store. 
General wisdom is to use Secrets Manager to store passwords, but you get the same security for free with Secure Strings in Parameter Store.

1. Navigate to **Systems Manager**
1. Under **Parameter Store**, select **Create parameter**
1. Complete the fields:
	- Name: 
	- Tier: Standard
	- Type: SecureString
	- Value: **M@d$ecur3P@ssw0rd**

# 1. Database

We'll first create an RDS instance for the database for our wiki.
I have selected the most cost effective values here to keep the bill low. Best practice and performance should be followed but isn't required to get up and running.

## 1.1 Create RDS Instance

1. Navigate to **Amazon RDS**
1. On the dashboard, click **Create Database**
1. Complete the form
	- Choose a database creation method: **Standard Create**
	- Engine type: **PostgreSQL**
	- Engine Version: **Default (14.6 today)**
	- Templates: **Free tier**
	- DB instance identifier: **wikijs**
	- Master username: **postgres**
	- Master password: the value used in ***wikijs-db-password*** parameter
	- DB instance class: Burstable classes - **db.t4g.micro**
	- Storage type: **General Purpose SSD (GP3)**
	- Allocated storage: **20**
1. Click **Create Database**

## 1.2 Configure Database

Log onto an EC2 instance with access to the database using your favourite PostgreSQL client then create the database.
Here's an example using an Amazon Linux 2 instance
```
# Enable extra packages
sudo amazon-linux-extras install postgresql14

# Install postgresql client
sudo yum install postgresql

# Get IP of RDS instance
host wikijs.random.region.rds.amazonaws.com

# Connect to database
psql "sslmode=disable dbname=postgres user=postgres hostaddr=10.1.0.113"

# Create wikijs database 
CREATE DATABASE wikijs;
```

# Elastic Container Service

Amazon Elastic Container Service (Amazon ECS) is a fully managed container orchestration service that helps you easily deploy, manage, and scale containerized applications. 

I've used the smallest possible values here to control costs but ECS allows easy vertical and horiztonal capacity scaling should you ever have the need.

## Create Task

A task definition is required to run Docker containers in Amazon ECS.

1. Navigate to **Amazon ECS**
1. Under Task definitions, click **Create new task definition**
1. Complete the fields for **Container 1**
	- Task definition family: **wikijs**
	- Container details:
		- Name: **wikijs-2**
		- Image URI: **ghcr.io/requarks/wiki:2**
	- Port mapping
		- Container port: **3000**
		- Protocol: **TCP**
		- Port name: **wikijs-3000-tcp**
		- App protocol: **HTTP**
	- Environmental Variables

	| Key		   | Type     	| Value                                |
	|----------|------------|--------------------------------------|
	| DB_TYPE  | Value      | postgres                             |
	| DB_SSL   | Value   	  | false                                |
	| DB_PORT  | Value      | 5432                                 |
	| DB_HOST  | Value      | wikijs.blah.region.rds.amazonaws.com |
	| DB_NAME  | Value      | wikijs                               |
	| DB_USER  | Value      | postgres                             |
	| DB_PASS  | ValueFrom  | wikijs-db-password (parameter path   |
	{.dense}

1. Complete the fields for **Environment**
	- Task size: **.25 vCPU** and **.5GB memory**

## Create Cluster

An Amazon ECS cluster is a logical grouping of tasks or services.

1. Navigate to **Amazon ECS**
1. Under **Clusters**, click **Create Cluster**
1. Complete the fields
	- Cluster name: **wikijs**
	- VPC: **your-vpc-id**
	- Subnets: **pick two**
	- Infrastructure: **AWS Fargate (serverless)**
1. Click **Create Cluster**

## Create Service

An Amazon ECS service is used to run and maintain a specified number of instances of a task definition simultaneously in a cluster. If one of your tasks fails or stops, the service scheduler launches another instance of your task definition to replace it. This helps maintain your desired number of tasks in the service.

We will be deploying an Elastic Load Balancer as part of the service. The load balancer to be the public presence of our wiki on the internet. It will also distributes traffic across the tasks if you decide to scale beyond a single container for high availability.

Once your cluster is created, click **Create** under the **Services** tab.
Use the following values:

1. Environment
	- Compute options: **Launch Type**
	- Launch type: FARGATE
	- Platform version: LATEST

1. Deployment configuration
	- Application type: **Service**
	- Family: **wikijs**
	- Revision: **Latest**
	- Service name: wikijs
	- Desired tasks: **1**

1. Networking
	-	Security group: **wikijs-elb**
	- Public IP: **turned off**

1. Load balancing
	- Load balancer type: **Application Load Balancer**
	- Application Load Balancer: **Create a new load balancer**
	- Load balancer name: **wikijs-public**
	- Listener: **Create new listener**
	- Port: **80**
	- Target group: **Create new target group**
	- Target group name: **wikijs-workers**
	- Protocol: HTTP

Click **Create**

Once the container has downloaded and started running your cluster should have 1 service and 1 running task. Click into the task and drill down to review logs if anything appears to be not working.

Head on over to **EC2** service, under **Load Balancers**, you should see your new load balancer listed. Copy the DNS name and paste it into a browser e.g. http://wikijs-alb-random.elb.eu-west-1.amazonaws.com

# What Next?

You should now be up and running with WikiJS but if you have time to spare consider the following tasks...

- Get yourself a free SSL certificate from [Certificate Manager](https://docs.aws.amazon.com/acm/latest/userguide/acm-overview.html) and apply it to your load balancer
- Configure automatic backups for your database
- Add [Web Application Firewall](https://docs.aws.amazon.com/waf/latest/APIReference/Welcome.html) to the load balancer
