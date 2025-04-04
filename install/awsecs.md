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
We'll use Elastic Container Service to run the container and the Relational Database Service for the MySQL database. 

Alternatively, you could run everything on a single EC2 instance, but this setup is already covered in the Linux installation guide.

By the end of this, we'll deploy;
- An Amazon RDS MySQL instance
- A Secret in AWS Secrets Manager
- An ECS cluster, service, and task running the WikiJS container
- An Application Load Balancer

> Please note WikiJS will move to PostgreSQL exclusively. https://beta.js.wiki/blog/2021-wiki-js-3-going-full-postgresql
{.is-warning}

# Prerequisites

1. An AWS account
1. Existing VPC with at least two subnets

# Secrets Manager

We will use Secrets Manager to store our Database master password following best practices.

1. Navigate to **Secrets Manager**
1. Click **Store a new secret**
1. Secret type
	- **Other type of secret** (Credentials for Amazon RDS database could be used, but won't be for simplicity in this guide)
1. Key/value pairs
	- Select **Plaintext**
   	- Write: **\<Your Password>**
1. Click **Next**
1. Secret Name and description
	- Secret Name: **wikijs/mysql**
1. Click **Next**
1. Click **Next**
1. Click **Store**
1. Navigate to the secret (you may need to refresh)
1. Grab the **Secret ARN**


# Security Groups

We will need two security groups, one for the load balancer and another for the database.

1. Navigate to **EC2**
1. Select **Security Groups** (In the navigation column on the left under "Network & Security")

## Load Balancer Security Group

1. Click **Create Security Group**
1. Basic details
	- Security group name: **wikijs-elb**
	- Description: **Security Group for WikiJS Load Balancer**
	- VPC: Select your **VPC**
1. Inbound rules
	- Click **Add Rule**
  	- Type: **HTTP**
	- Source: **Anywhere-IPV4** (0.0.0.0/0)
	- Description: **HTTP to WikiJS**
	- Click **Add Rule**
  	- Type: **Custom TCP**
     	- Port range: **3000**
	- Source: **Anywhere-IPV4** (0.0.0.0/0)
	- Description: **HTTP to WikiJS**
1. Click **Create Security Group**

## Database Security Group

1. Click **Create Security Group**
1. Basic details
	- Security group name: **wikijs-database**
	- Description: **Security Group for WikiJS Database**
	- VPC: Select your **VPC**
1. Inbound rules
	- Click **Add Rule**
  	- Type: **MYSQL/Aurora**
	- Source: **Custom** and your **wikijs-elb** Security Group
	- Description: **MySQL access for WikiJS**
1. Click **Create Security Group**

# IAM

We will need a custom IAM Policy and Role.

## IAM Policy

We need to make a custom IAM Policy to specifically grant access to the Secret we made prior.

1. Navigate to the **IAM** service
1. Select **Policies** (In the navigation column on the left under "Access Management")
1. Click **Create Policy**
1. Policy Editor
	- Select **JSON**
	- Write:
>	 { <br>
	"Version": "2012-10-17",<br>
	"Statement": [<br>
		{<br>
			"Effect": "Allow",<br>
			"Action": "secretsmanager:GetSecretValue",<br>
			"Resource": "**wikijs/mysql Secret ARN**"<br>
		}<br>
	]<br>
}
1. Click **Next**
1. Policy details
	- Policy name: **WikiJS-Secret-Access**
1. Click **Create policy**

## IAM Role

We will need an IAM Role to provide our containers access to our secret.

1. Navigate to the **IAM** service
1. Select **Roles** (In the navigation column on the left under "Access Management")
1. Click **Create Role**
1. Trusted entity type: 
	- Select: **AWS Service**
1. Use case 
	- Service or use case: **Elastic Container Service**
 	- user case: **Elastic Container Service Task**
1. Click **Next**
1. Add permissions
	- Find and select **WikiJS-Secret-Access**
	- Find and select **AmazonECSTaskExecutionRolePolicy**
1. Click **Next**
1. Role details
	- Role name: **WikijsTaskExecutionRole**
1. Click **Create Role**


# Database

We'll need to create an RDS instance for the database for our wiki.

This is a simple setup guide, therefore options chosen are cost effective and not necessarily following best practices.

## Create RDS Instance

1. Navigate to **Amazon RDS**
1. On the dashboard, click **Create Database**
1. Creation Method
   	- Standard create
1. Engine Options
	- Engine type: **MySQL**
	- Engine Version: **Default (8.0.40 today)**
1. Templates
	- Templates: **Free tier**
1. Settings
	- DB instance identifier: **wikijs-db**
	- Master username: **wikijs_db_admin**
	- Master password: the value used in the **wikijs/mysql** secret
1. Instance Configuration
	- DB instance class: Burstable classes - **db.t4g.micro**
1. Storage
	- Storage type: **General Purpose SSD (gp2)**
	- Allocated storage: **20**
1. Connectivity
	- Virtual Private Cloud: Select your **VPC**
	- DB Subnet Group: Select your **subnet group**
	- VPC Security Group: **wikijs-database**
1. Additional Configuration
   	- Initial database name: **wikijs**
1. Click **Create Database**

Note: Settings not mentioned can largely be left as default values.

# Elastic Container Service

Amazon Elastic Container Service (Amazon ECS) is a fully managed container orchestration service that helps you easily deploy, manage, and scale containerized applications. 

ECS requires three main parts, a Task Definition, a Cluster, and a Service. We will make them in that order. 

I've used the smallest possible values here to control costs but ECS allows easy vertical and horizontal capacity scaling should you ever have the need.

## Create Task

A task definition is required to run Docker containers in Amazon ECS.

1. Navigate to **Amazon ECS**
1. Under Task definitions (on the left navigation column), click **Create new task definition**
1. Task Definition Configuration
   	- Task Definition Family Name: **wikijs**
1. Infrastructure Requirements
   	- Launch Type: **Fargate**
   	- Operating System/Architecture: **Linux/X86_64**
   	- CPU: **.25 vCPU**
   	- Memory: **.5 GB**
   	- Task Execution Role: **WikijsTaskExecutionRole**
1. Container - 1
	- Name: **wikijs-container**
	- Image URI: **requarks/wiki:2.5**
	- Port mapping:
		- Container port: **3000**
		- Protocol: **TCP**
		- Port name: **wikijs-3000-tcp**
		- App protocol: **HTTP**
	- Environmental Variables:

	| Key		   | Type     	| Value                                |
	|----------|------------|--------------------------------------|
	| DB_TYPE  | Value      | mysql                             |
	| DB_PORT  | Value      | 3306                                 |
	| DB_HOST  | Value      | \<Wikijs-db endpoint URL> |
	| DB_NAME  | Value      | wikijs                               |
	| DB_USER  | Value      | wikijs_db_admin                             |
	| DB_PASS  | ValueFrom  | \<wikijs/mysql secret ARN>   |
	{.dense}

1. Create

## Create Cluster

An Amazon ECS cluster is a logical grouping of tasks or services.

1. Navigate to **Amazon ECS**
1. Under **Clusters** (on the left navigation column), click **Create Cluster**
1. Cluster Configuration
	- Cluster Name: **wikijs-cluster**
1. Create

## Create Service

An Amazon ECS service is used to run and maintain a specified number of instances of a task definition simultaneously in a cluster. If one of your tasks fails or stops, the service scheduler launches another instance of your task definition to replace it. This helps maintain your desired number of tasks in the service.

We will be deploying an Elastic Load Balancer as part of the service. The load balancer to be the public presence of our wiki on the internet. It will also distributes traffic across the tasks if you decide to scale beyond a single container for high availability.

Once your cluster is created, click **Create** under the **Services** tab.
Use the following values:

1. Environment
	- Compute options: **Launch Type**
	- Launch type: **FARGATE**
	- Platform version: **LATEST**
1. Deployment configuration
	- Task Definition Family: **wikijs**
	- Revision: **Latest**
	- Service name: **wikijs-service**
	- Desired tasks: **1**
1. Networking
	- VPC: **\<Your VPC>**
	- Subnets: **\<Your Subnet(s)>**
 	- Security group: **wikijs-elb**
	- Public IP: **turned on**
1. Load balancing
	- Check **Use Load Balancing**
	- Load balancer type: **Application Load Balancer**
	- Application Load Balancer: **Create a new load balancer**
	- Load balancer name: **wikijs-public**
	- Listener: **Create new listener**
	- Port: **80**
	- Target group: **Create new target group**
	- Target group name: **wikijs-workers**
	- Protocol: HTTP
1. Create

Once the container has downloaded and started running your cluster should have 1 service and 1 running task. Click into the task and drill down to review logs if anything appears to be not working.

Head on over to **EC2** service, under **Load Balancers**, you should see your new load balancer listed. Copy the DNS name and paste it into a browser e.g. http://wikijs-alb-random.elb.eu-west-1.amazonaws.com

# What Next?

You should now be up and running with WikiJS but if you have time to spare consider the following tasks...

- Get yourself a free SSL certificate from [Certificate Manager](https://docs.aws.amazon.com/acm/latest/userguide/acm-overview.html) and apply it to your load balancer.
- Configure automatic backups for your database.
- Configure autoscaling.
- Add [Web Application Firewall](https://docs.aws.amazon.com/waf/latest/APIReference/Welcome.html) to the load balancer.
