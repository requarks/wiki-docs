---
title: Git
description: Storage Module
published: true
date: 2023-03-09T13:21:52.320Z
tags: storage, module
editor: markdown
dateCreated: 2023-01-08T10:37:11.629Z
---

Git is a version control system for tracking changes in computer files and coordinating work on those files among multiple people.
Git是一种版本控制系统，用于跟踪计算机文件的更改并协调多人在这些文件上的工作。

# 开始使用

可能是存储文档最流行的方法，Git模块可以轻松地与任何远程Git仓库同步。

为了方便起见，下面列出了最流行的Git提供商的说明。然而，该模块应该适用于几乎任何标准的Git提供商。

**您必须在系统上安装Git 2.7.4或更高版本才能启用此模块！**
*docker镜像已经包含了此依赖项。*

*Git存储库必须专门用于Wiki.js。目前无法仅使用子文件夹或子模块。*

Probably the most popular way to store documentation, the Git module can effortlessly synchronize with any remote Git repository.

For convenience, instructions for the most popular Git providers are listed below. However, this module should work for virtually any standard Git provider.

**You must have Git 2.7.4 or later installed on the system to enable this module!**
*The docker image already contains this dependency.*

*A Git repository must be dedicated to Wiki.js. It is not possible to use only a subfolder or submodules at the moment.*

# 提供商

## Azure DevOps

*即将上线*

## BitBucket

*即将上线*

## GitHub

[GitHub](https://www.github.com) 是最受欢迎的git版本控制提供商

### 生成一个新密钥

1. 启动终端
2. 键入以下命令：
   ```bash
   ssh-keygen -t rsa -b 4096
	 ```
3. 在提示保存生成的文件时，输入一个Wiki.js可以访问的路径（例如 `/etc/wiki/github.pem`），然后按下 **Enter**。
4. 将密码留空，然后按两次 **Enter**。受密码保护的密钥将无法使用。


> 在Windows上，您可以使用 [Git Bash](https://git-scm.com/download/win) 或Windows下的Linux子系统发行版（例如 [适用于Windows的Ubuntu](https://www.microsoft.com/en-us/p/ubuntu/9nblggh4msv6)）来运行上面的命令。您也可以使用[puttygen](https://www.ssh.com/ssh/putty/download) 手动生成密钥。
{.is-info}

### 将密钥添加到GitHub

1. 创建一个新的GitHub存储库。
1. 点击**设置**选项卡。
1. 点击左侧导航菜单中的**部署密钥**。
1. 点击**添加部署密钥**按钮。
1. 为此密钥输入一个您选择的名称（例如 wiki），并粘贴先前生成的公钥的内容。*(以 .pub 结尾的文件)*
1. 确保勾选**允许写入**。
1. 点击**添加密钥**按钮。

1. Create a new GitHub repository.
2. Click on the **Settings** tab.
3. Click on the **Deploy Keys** in the left navigation menu.
4. Click the **Add deploy key** button.
5. Enter a name of your choice for this key (e.g. wiki) and paste the contents of the public key generated earlier. *(file ending in `.pub`)*
6. Make sure the **Allow write access** is checked.
7. Click the **Add key** button.

### 配置Wiki.js

1. 在管理区中，点击左侧导航菜单中的**存储**选项。
1. 确保选中**Git**为存储目标。
1. 点击**Git**选项卡。
1. 输入以下设置：
	- 认证类型：`ssh`
  	- 存储库URI：*在您的GitHub存储库页面的**Code**选项卡中，点击**Clone or download**绿色按钮，并复制下方**Clone with SSH**显示的URI。*
  	- 分支：`main`
  	- SSH私钥路径：*之前生成的私钥路径*
  	- 用户名：*留空*
  	- 密码：*留空*
  	- 默认作者E-mail：*应与您的GitHub账户的电子邮箱相匹配。*
  	- 默认作者名：*应与您的GitHub账户名称匹配。*
  	- 本地存储库路径：*选择将存储库克隆到本地的位置，或保留默认值`/data/repo`*
    - 验证SSL证书：**开启**
  
1. 将 **同步方向** 设置为 **双向**。
1. 将 **同步计划** 设置为 **每5分钟**。
1. 点击页面顶部的 **应用更改** 按钮。
1. 等待 **状态** 面板更新。一个新的 Git 条目应该以绿色显示。如果条形图为红色，则意味着您的配置中有错误。返回到Git选项卡，修复错误并重试。

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

*即将上线*

# 一般情况

## 重要提示

当首次启用Git存储模块并配置一个已有内容的存储库是，您可能需要执行手动倒入。默认情况下，将仅导入本地最新提交和远程最新提交之间的更改。
When enabling the Git storage module for the first time with a remote repository that already has content, you might need to initiate a manual import. By default, only changes between the latest local commit and the latest remote commit will be imported.

> **注意！** 在继续下面的步骤之前，请确保Git模块已经配置好并正常工作。
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
