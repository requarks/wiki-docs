---
title: Migrate from Wiki.js v1.x
description: How to import content and users from an older v1.x installation.
published: true
date: 2019-10-26T16:34:59.862Z
tags: 
---

# Overview

In order to upgrade from an older 1.x version of Wiki.js, you need to first install Wiki.js 2.x using the standard [installation instructions](/install).

Because of the significant architecture differences between v1 and v2, **you cannot do an in-place upgrade**.
You need to first do a fresh v2 installation from which you'll import content, uploads and users into.

Once your new v2 installation is working, follow the instructions below to bring content, uploads and users from your older v1 installation into your new v2 installation.

# Import

1. Navigate to the **Administration Area** *(click your avatar at the top right of the page)*.
1. Click on **Utilities** in the left sidebar navigation.
1. Click on **Import from Wiki.js 1.x**.
1. Select whether you want to import **Content + Uploads**, **Users** or both.

## Content + Uploads

If you were using a remote Git repository to sync content to in your v1 installation, choose **Import from Git connection**.
Otherwise, choose **Import from local folder**.

### Import from Git connection

Enter all the required connection information to connect to your remote Git repository. These settings should be the same as the one entered in your v1 `config.yml` file under the **git** section.

If using the **SSH** authentication method, you'll need to copy the contents of the file you were referencing in v1 into the **Private Key Contents** field.

> :warning: **WARNING**
>
> For most scenarios, you should leave the default value of `./data/repo` for the **Local Repository Path** field. This folder should be empty and dedicated to v2.
> **DO NOT** point to your current v1 local repository folder.
{.is-danger}

### Import from local folder

Enter the path to the local repository folder used in your v1 installation.

## Users

Enter the MongoDB database connection string, as entered in your v1 installation `config.yml` file.

Select how groups and permissions should be created. *It's recommended to use the first option which will put users that have the same permissions into the same group.*

## Start Import

When ready, click the **Start Import** button to initiate the migration process. You'll be notified of any failure in importing content and a list of users that could not be imported will be displayed.

> It's safe to retry the migration process as many times as needed. No duplication will occur as users that already exists will be skipped and content will be updated.
{.is-info}

# Post-migration

Once the migration is completed and you've verified that content, uploads and users were successfully copied over, make sure to read the following recommendations:

- If you've imported content using the **Import from Git connection** option, it's recommended that you shutdown your v1 installation. While it's possible to run both v1 and v2 installations connected to the same Git repository in parallel, you should ensure that editing is only done on one of them. Editing the same page on both installations within the same time frame can result in merge conflicts.
- If you've imported content using the **Import from local folder** option, it's highly recommended to change the path so that it no longer points to your v1 installation. To do so, click on **Storage** in the left sidebar navigation, then click on **Local File System**. Change the path to something else (e.g.: `./data/content`). Additionally, unless you want content to be exported to disk on change, you may disable the **Local File System** storage module completely.

