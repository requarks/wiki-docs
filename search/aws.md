---
title: AWS CloudSearch
description: Search Engine Module
published: true
date: 2019-09-15T02:43:38.607Z
tags: 
---

Amazon CloudSearch is a managed service in the AWS Cloud that makes it simple and cost-effective to set up, manage, and scale a search solution for your website or application.

# Setup

## Create the Search Domain

1. Login to your [AWS Console](https://console.aws.amazon.com)
1. Create a new **CloudSearch** domain.
1. Name your domain, choose the desired instance type and click **Continue**.
1. At the **Configure Index** step, select **Manual Configuration**. Click **Continue**.
1. At the **Review Index Configuration** step, leave everything empty and click **Continue**.
1. Enter an Access Policy and **Continue**. It's recommended to limit by the IP of the server onto which Wiki.js is installed.
1. Finally create the domain.

## Create the Search User

1. In [IAM](https://console.aws.amazon.com/iam), click on **Users**.
1. Click on **Add User**.
1. Enter a **User name** (e.g. wikisearch) and make sure **Programmatic access** is enabled. Click on **Next: Permissions**.
1. Choose **Attach existing policies directly** and search for **CloudSearchFullAccess** and select it.
1. Continue through the next steps to create the user.
1. Make note of the **Access Key ID** and the **Secret Access Key**.

## Configure in Wiki.js
1. In the Wiki.js administration area, click on **Search Engine** in the sidebar.
1. Select **AWS CloudSearch** as the search engine.
1. Enter the **Search Domain** of the AWS CloudSearch domain you just created. This is the name you entered when creating the new domain.
1. Enter the **Document Endpoint**, found in the dashboard of the search domain in the AWS console.
1. Select the **Region** where the search domain was created.
1. Enter the **Access Key ID** and **Secret Access Key** generated earlier.
1. Select the language to use for the Analysis Scheme.
1. Click the **Apply** button to save and initialize the search engine. An index will be created automatically.

Note that if you already have content in your wiki, you must click on **Rebuild Index** afterwards to import all your existing content into the search engine. Any change (new, edit, delete page) will be handled automatically from this point forward.