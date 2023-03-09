---
title: Git
description: Storage Module
published: true
date: 2021-03-21T00:41:57.739Z
tags: module, storage
editor: markdown
dateCreated: 2019-02-17T22:58:31.273Z
---

Git is a version control system for tracking changes in computer files and coordinating work on those files among multiple people.

# Getting Started

Probably the most popular way to store documentation, the Git module can effortlessly synchronize with any remote Git repository.

For convenience, instructions for the most popular Git providers are listed below. However, this module should work for virtually any standard Git provider.

**You must have Git 2.7.4 or later installed on the system to enable this module!**
*The docker image already contains this dependency.*

*A Git repository must be dedicated to Wiki.js. It is not possible to use only a subfolder or submodules at the moment.*

# Providers

## Azure DevOps

*Coming soon!*

## BitBucket

*Coming soon!*

## GitHub

[GitHub](https://www.github.com) is the most popular git source control provider.

### Generate a new key

1. Open Terminal.
2. Enter the command:
   ```bash
   ssh-keygen -t rsa -b 4096
	 ```
3. When prompted to save the generated file, enter a path which can be accessed by Wiki.js *(e.g. `/etc/wiki/github.pem`)* and press **Enter**.
4. Leave the passphrase empty and press **Enter** twice. Password-protected keys will NOT work.

> On Windows, you can use [Git Bash](https://git-scm.com/download/win) or Windows Subsystem for Linux (WSL) distributions like [Ubuntu for Windows](https://www.microsoft.com/en-us/p/ubuntu/9nblggh4msv6) to run the commands above. You can also generate keys manually using the [puttygen](https://www.ssh.com/ssh/putty/download) utility.
{.is-info}

### Add the key to GitHub

1. Create a new GitHub repository.
2. Click on the **Settings** tab.
3. Click on the **Deploy Keys** in the left navigation menu.
4. Click the **Add deploy key** button.
5. Enter a name of your choice for this key (e.g. wiki) and paste the contents of the public key generated earlier. *(file ending in `.pub`)*
6. Make sure the **Allow write access** is checked.
7. Click the **Add key** button.

### Configure Wiki.js

1. In the Administration Area, click on **Storage** in the left navigation menu.
2. Make sure the **Git** storage target is checked.
3. Click on the **Git** tab.
4. Enter the following settings:
   - Authentication Type: `ssh`
   - Repository URI: *On your GitHub repository page, in the **Code** tab, click on the **Clone or download** green button and copy the URI shown below **Clone with SSH**.*
   - Branch: `main`
   - SSH Private Key Path: *The path to your private key generated earlier.*
   - Username: *Empty*
   - Password: *Empty*
   - Default Author Email: *Should match your GitHub account email.*
   - Default Author Name: *Should match your GitHub account name.*
   - Local Repository Path: *Choose where the repo will be cloned locally or leave the default `./data/repo` value.*
   - Verify SSL Certificate: **On**
5. Set the **Sync Direction** to **Bi-directional**.
6. Set the **Sync Schedule** to **5 minutes**.
7. Click the **Apply Changes** button at the top of the page.
8. Wait for the **Status** panel to update. A new entry for **Git** should appear in green. If the bar is red, it means you have an error in your configuration. Go back to the Git tab, fix the error and try again.

## GitLab

*Coming soon!*

# Common Scenarios

## Import Content

When enabling the Git storage module for the first time with a remote repository that already has content, you might need to initiate a manual import. By default, only changes between the latest local commit and the latest remote commit will be imported.

> **Heads up!** Make sure the Git module is already configured and working before proceeding any further!
{.is-warning}

To force an import of all content currently present in the local repository, load the **Git** module settings tab in the Administration Area (under **Storage**), scroll to the very bottom of the page and click **Run** button on the **Import Everything** action card.

## Missing Content in Remote Repository

If content was created in Wiki.js before you enabled the Git storage module or if you temporarily disabled the module, that content will be missing from the remote Git repository.

> **Heads up!** Make sure the Git module is already configured and working before proceeding any further!
{.is-warning}

To fix this issue, load the **Git** module settings tab in the Administration Area (under **Storage**), scroll to the very bottom of the page and click **Run** button on the **Add Untracked Changes** action card. This will force all content currently in the DB to be output to files in the local repository, add these files to git tracking and create a single commit.

Note that this will not perform a sync with your remote repository. You must either wait for the next synchronization to occur, or manually force a sync using the **Force Sync** action.

# Frequently Asked Questions

## Why content is not synced when I save a page?

For performance reasons, new commits are only synced on a regular interval (every 5 minutes by default). You can change the schedule in the **Git** storage module settings.

## How can I force a manual sync?

Load the **Git** module settings tab in the Administration Area (under **Storage**), scroll to the very bottom of the page and click **Run** button on the **Force Sync** action card.

![](https://static.requarks.io/logo/git-alt.svg =x70){.align-abstopright}
