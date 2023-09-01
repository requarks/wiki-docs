---
title: Azure Web App
description: Installation Guide
published: true
date: 2023-09-01T02:32:54.266Z
tags: setup, guide
editor: markdown
dateCreated: 2019-05-31T22:40:09.408Z
---

> This guide was contributed by the community and may be incomplete or become outdated.
{.is-warning}

This guide details the step-by-step procedure to install Wiki.js on an **Azure Web App** with an **Azure Database for PostgreSQL**.

# 1. Database

We'll first create the database for our wiki.

While it's possible to host the database alongside the application on the Azure Web App, this is not recommended as it will impact performance and is not scalable.

## 1.1 Create Database

1. Create a new resource, search for **Azure Database for PostgreSQL** and click **Create**.
1. Select **Single server**
1. Fill in the server details.
	- You must select a version of **9.6 or later**.
  	- The minimum server size is **Basic** with **1 vCore**, however you cannot upgrade to **General Purpose** afterwards if you choose Basic.
1. Finish by creating the resource.

## 1.2 Configure Database

1. Once the resource is created, navigate to **Connection security**.
1. Enable **Allow access to Azure services** so that your Azure Web App is able to access your DB.
1. Click on **Add client IP** to add your own IP address to the whitelist.
1. Click **Save** and wait for changes to be applied.

> :vertical_traffic_light: This guide assumes the DB will be dedicated to the wiki. If you plan on sharing the DB with other applications, you should connect to the server and create a dedicated user + database.
{.is-warning}

# 2. Azure Web App

We can now create the App Service where our wiki will run.

## 2.1 Create Web App

1. Create a new resource, search for **Web App** and click **Create**.
1. Fill in the instance details.
	- Select **Docker Image** for **Publish** type.
  	- Select **Linux** for **Operating System**.
    - The minimum App Service Plan size is **B1**. Consider selecting at least **P1V2** for production scenarios.
1. Click **Next: Docker**
1. Set the following options:
	- **Single Container**
  	- Image Source: **Docker Hub**
    - Access Type: **Public**
    - Image and Tag: `requarks/wiki:2`
1. Click **Review and create** (other steps are optional).

## 2.2 Configure Web App

1. Once the resource is created, navigate to **Configuration**.
1. Add the following **Application Settings**: *(replace `xyz` with values you entered when creating the DB earlier)*
	 ```
   DB_TYPE: postgres
   DB_HOST: xyz.postgres.database.azure.com
   DB_PORT: 5432
   DB_NAME: postgres
   DB_USER: xyz@xyz
   DB_PASS: xyz
   DB_SSL: true
   ```
1. Click **Save** to apply the configuration.
1. Navigate to the **Overview** tab and click **Restart**.
1. Wait for the container to be ready. You can monitor the app status in the **Container settings** tab, using the **Logs** window. A message similar to `Container xyz_0 for site xyz initialized successfully and is ready to serve requests.` should be logged.

# 3. Setup Wiki.js

1. Browse to your app public URL. *(Can be found in the **Overview** tab of your web app resource)*
1. Follow the instructions to create the admin account and start using your wiki.

# 4. Troubleshooting

## 4.1 431 Request Header Fields Too Large Issues 

Enabling **App Service Authentication** in **Azure** might cause `Request Header Fields Too Large` errors.  
To fix this:
1. In your Azure Web App, navigate to **Configuration**.
1. Add the following **Application Settings**:
   ```
   WEBSITE_AUTH_DISABLE_IDENTITY_FLOW: true
   ```

The issue can re-appear for graphql queries when enabling SAML 2.0 authentication in Wiki.js, even with above fix.  
To solve that we need to increase the max header size for NodeJS.
1. In your Azure Web App, navigate to **Configuration**.
1. Add the following **Application Settings**:
   ```
   NODE_OPTIONS: --max-http-header-size=81920
   ```

![](https://a.icons8.com/cqaghpTd/Zi0crm/svg.svg){.align-abstopright}
