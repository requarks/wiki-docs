---
title: 在AWS上安装
description: 
published: true
date: 2023-02-09T05:15:52.848Z
tags: setup, guide
editor: markdown
dateCreated: 2023-01-08T10:35:43.650Z
---

# 概述
AWS 应用市场的 Wiki.js映像是一套预先配置好的环境，由Wiki.js的开发人员制作，包含开始使用Wiki.js所需的一切。

## 映像规格

预装了以下软件的Ubuntu 18.04 LTS：

- Docker
- PostgreSQL 11 *(docker化)*{.caption}
- Wiki.js 2.x *(docker化, 可从80端口访问)*{.caption}
- Wiki.js Update Companion *(docker化)*{.caption}
- OpenSSH和预先配置了SSH、HTTP和HTTPS规则的UFW防火墙

## 实例类型

Wiki.js至少需要**t3.micro**实例大小，*不支持**t3.nano**实例类型*{.red--text}

但是，为了获得最佳性能，我们建议至少使用**t3.small**或更大的**c5.larget**实例大小。Wiki.js将后台进程用于CPU密集型任务（例如页面渲染）。因此，拥有至少2个专用CPU内核将提高此类任务的性能。

# 开始安装

1. 在AWS 应用市场上的[Wiki.js产品页面](https://aws.amazon.com/marketplace/pp/B0832LDTKQ)，单击页面顶部的**继续订阅**按钮。
1. 按照屏幕上的说明启动实例。
1. 实例运行后，转到AWS管理控制台中的实例详细信息。
1. 复制实例的**公共DNS**endpoint。
1. 在新的浏览器选项卡中，导航到http://YOUR-PUBLIC-DNS *（替换为您的公共DNS endpoint或IP）*
  > **服务器开始接受请求可能需要几分钟的时间。**在您能够访问wiki之前，必须首先初始化各种服务。如果第一次尝试时未加载，请等待5分钟，然后重试。
  {.is-info}
1. 此时应该会出现Wiki.js的设置屏幕。为管理员帐户输入所需的**电子邮件地址**和**密码**。
1. 输入wiki的**完整URL**，不带结尾的斜杠。建议将子域/域指向您的公共IP（例如wiki.example.com）。如果您还没有设置域名，则可以使用您的公共DNS endpoint或IP作为URL（例如。http://xx.xx.xx.xx). 这可以稍后在**管理区域**（在**常规**部分下）中更改。
1. 单击**安装**以完成安装。完成后，您将自动重定向到登录页面。输入您先前输入的管理员帐户的电子邮件和密码。

# 使用Let's Encrypt自动部署HTTPS

> 在启用Let's Encrypt**之前**，您必须完成安装向导（参见[开始安装](#开始安装)）！
{.is-warning}

1. 在域注册商上创建一个**A记录**，以将域/子域（例如wiki.example.com）指向您的EC2实例**公共IP**。
2. 确保您能够使用HTTP上的域/子域（例如。http://wiki.example.com).
3. 通过**SSH**连接到您的EC2实例。
4. 运行以下命令，**停止**并**删除**现有wiki容器 *（不会丢失任何数据）*：

```bash
docker stop wiki
docker rm wiki
```

5. 替换`wiki.example.com`和`admin@example.com`为**您自己的域/子域**和wiki管理员的**电子邮件地址**的值，执行以下命令：

```bash
docker create --name=wiki -e LETSENCRYPT_DOMAIN=wiki.example.com -e LETSENCRYPT_EMAIL=admin@example.com -e SSL_ACTIVE=1 -e DB_TYPE=postgres -e DB_HOST=db -e DB_PORT=5432 -e DB_PASS_FILE=/etc/wiki/.db-secret -v /etc/wiki/.db-secret:/etc/wiki/.db-secret:ro -e DB_USER=wiki -e DB_NAME=wiki -e UPGRADE_COMPANION=1 --restart=unless-stopped -h wiki --network=wikinet -p 80:3000 -p 443:3443 requarks/wiki:2
```

6. 执行以下命令，启动容器
```bash
docker start wiki
```

7. **等待**容器启动，Let's Encrypt配置过程完成。您可以通过运行以下命令查看容器日志：
```
docker logs wiki
```
> 当您在日志中看到以下行时，代表过程完成：
>
> `(LETSENCRYPT) New certifiate received successfully: [ COMPLETED ]`
> `HTTPS Server on port: [ 3443 ]`
> `HTTPS Server: [ RUNNING ]`
{.is-success}

8. 使用HTTPS连接（例如。https://wiki.example.com)。 您的wiki现在可以使用免费Let's Encrypt证书接受HTTPS请求！

## 自动重定向HTTP到HTTPS

默认情况下，对HTTP端口的请求不会重定向到HTTPS。您可以使用以下说明启用此选项：

1. 击页面右上角的头像，导航到**管理区域**。
2. 左侧导航菜单中，单击**SSL**。
3. 在“将HTTP请求重定向到HTTPS”部分旁边，单击**打开**以启用HTTP到HTTPS重定向。
4. HTTP端口的任何请求现在都将自动重定向到HTTPS！

## 更新证书

您可以随时从**管理区***>**SSL**续订证书。

如果您的证书已过期，并且无法加载Wiki UI来续订，只需重新启动容器：

```bash
docker restart wiki
```

更新过程将在初始化期间自动运行。

# 升级

这个映像附带Wiki.js Update Companion，当新版本可用时，它可以自动执行升级过程。

当新版本可用时，您将在**管理区**中收到通知。要执行升级，请遵循以下简单说明：
1. 转到**系统信息**部分，然后单击**执行升级**按钮。
1. 等待升级完成
1. 您现在应该可以使用最新版本。就这么简单！

![](https://static.requarks.io/logo/aws.svg){.align-abstopright}