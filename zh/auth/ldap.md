---
title: LDAP / Active Directory
description: 身份认证模块
published: true
date: 2023-03-16T08:45:000Z
tags: auth, module, 模块, 身份认证
editor: markdown
dateCreated: 2023-01-08T10:34:25.546Z
---

LDAP/Active Directory是Microsoft开发的企业身份验证解决方案。

# 配置

1. 在您wiki的 **管理区**中，点击左侧导航栏中的 **身份验证**。
1. 点击 **LDAP / Active Directory**.
1. 输入可访问的 **LDAP URL**
1. 在用于绑定的账户的**管理员绑定DN**中输入可识别的名称。
1. 在上面指定的账户的**管理员绑定凭据**中输入密码。
1. 在**搜索基准**字段中输入要在其中搜索用户的基准DN。
1. 在**搜索筛选**字段中输入用于匹配用户与用户名/email的筛选语句。输入的值必须含有`{{username}}`标签。例如，若用户名存储与`uid`字段中，对应的筛选语句为`(uid={{username}})`。在执行搜索时，`{{username}}`标签将在执行匹配时被替换为对应的用户名。
1. 如果LDAP服务端要求必须提供TLS证书，请启用**使用TLS**选项并在**TLS证书路径**中输入TLS证书的绝对路径。
1. 如果您的directory字段与Wiki.js使用的directory字段不同，您可以使用以下字段为每个directory字段指定映射：
	- **Unique ID 字段映射**
  	- **Email 字段映射**
  	- **Display Name 字段映射**
  	- **Avatar Picture 字段映射**
1. 启用 **开放注册** 选项 *(除非您希望人工验证每一个用户)*。
1. 选择用户首次登陆时会被分配到的**用户组**。
1. 确保**LDAP / Active Directory**旁边的复选框为已勾选状态。您现在应该可以看到文字提示此策略处于**启用**状态。
1. 点击此页右上角的**应用**以保存并应用设置。

# 测试配置

Saving your LDAP configuration doesn't actually perform a connection to your LDAP Server. You need to perform an actual login to establish a connection.

To do so, open an incognito window in your browser and attempt to login to your wiki with a user in your directory.

保存LDAP配置并未执行到LDAP服务器的连接。您需要进行实际登录以建立连接。

为此，请在浏览器中打开一个无痕浏览窗口，并尝试使用目录中的用户登录到wiki。

# 疑难解答
如果在尝试登录时出现错误，可以启用LDAP调试标志以向控制台（或docker日志）报告内部LDAP错误消息。

If you get errors while trying to login, you can enable a LDAP debugging flag to report internal LDAP error messages to the console (or docker logs).

在 **管理区**中, 点击侧边栏内的 **开发者工具**, 转到**标志**. 启用**LDAP Debug** 标志.

> 如果您使用docker，输入命令 `docker logs wiki` 来查看日志 *(假定您的容器名是`wiki`)*. 
{.is-info}

