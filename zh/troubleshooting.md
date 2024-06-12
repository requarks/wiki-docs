---
title: 常见问题
description: 常见问题和解决方案
published: true
date: 2023-03-16T08:45:00.000Z
tags: setup, guide, 配置, 指南
editor: markdown
dateCreated: 2023-01-08T10:33:56.747Z
---

# 无法上传大小超过 X 的文件

**原因**： 这很有可能是因为你使用了反向代理（如nginx、apache）。它们的配置阻止了超过特定大小文件的上传。
**解决方案**： 在您使用的反向代理的配置文件中增大有关文件上传大小限制的参数。

# Cloudflare - JS / CSS / Emojis 无法加载

**原因**： CloudFlare在传输某些文件时执行了一些“优化”。这些优化破坏了文件内容与其完整性签名的一致性，进而被浏览器所阻止。

**解决方案**： 在您的Cloudflare面板上为您的站点创建一条新的页面规则。进入根目录`wiki.yourdomain.com/`，添加如下设置：

- **Auto Minify**: Uncheck all
- **Mirage**: Off
- **Rocket Loader**: Off

保存并部署上述页面规则。

# 在使用反向代理将网站置于子目录时出错

**原因**： Wiki.js 无法在子目录下安装和使用。

**解决方案**: 使用子域名。 （如： `wiki.yourcompany.com`）

# Error: Listening on port XX requires elevated privileges!

**原因**: 部分Linux会阻止Node.js绑定特定范围的端口 *(如：端口号低于1024的端口)*. 如果在config.yml中设置了位于阻止范围内的端口（例如80），就会发生这种情况。

**解决方案 A**: 允许node进程安全访问指定端口：

```bash
# Ubuntu / Debian

sudo apt-get install libcap2-bin
sudo setcap cap_net_bind_service=+ep `readlink -f \`which node\``
```

**解决方案 B**: 创建端口转发规则 *(下面的示例设置对应在config.yml中指定3000端口，并将经由网卡eth0、目标端口为80的流量转发至3000端口的配置)*

```bash
sudo iptables -t nat -A PREROUTING -i eth0 -p tcp --dport 80 -j REDIRECT --to-port 3000
```

**解决方案 C**: 使用web server程序。例如，使用nginx监听 80/443 端口并将所有请求转发到绑定至更高端口的Wiki.js （如：3000端口）。

# Error: Port XX is already in use!

**原因**: 另一个进程占用了你指定的端口。

**解决方案**: 为Wiki.js指定其他端口，或找到占用端口的进程（如：web server，http应用等）并终止它们。

# Error: Unknown authentication strategy "jwt"

**原因**: 当尝试在服务端完成初始化之前就访问网站时，就会出现此错误。

**解决方案**: 刷新页面即可。如果一段时间之后错误仍然存在，请检查服务端日志，查找阻碍Wiki.js完成初始化的错误。

# 如何在页面加载时执行JavaScript代码

您可能已经注意到，在标准页面加载或dom就绪事件上运行javascript代码不起作用，因为页面内容还没有被渲染。

你需要通过`window.boot.register(evt, clb)`注册一个触发事件为`page-ready`的回调函数，例如：

```js
window.boot.register('page-ready', () => {
	// code to execute
})
```

您的代码将在页面加载完毕、Vue实例就绪后执行。

# 如何隐藏页脚对Wiki.js的提及

**你认真的吗?** 本软件完全免费。贡献者们为这个项目投入了数千小时。我们觉得，作为回报，在页脚中的一个小小的提及是一件非常小的事情。。。

# 如何手动禁用HTTPS/SSL重定向

如果您因为SSL证书错误无法加载站点，您可以手动禁用SSL重定向。

在数据库的`settings`表中，你需要将`server`键的`sslRedir`属性改为否。
重启Wiki.js以应用设置更改。

### 如果你是Docker用户

如果你的PostgreSQL是在docker镜像中运行的话（如：DigitalOcean/AWS官方镜像），你可以执行如下命令：

```bash
docker exec db psql -U wiki -d wiki -c "DELETE FROM settings WHERE key = 'server';"
docker restart wiki
```

# 如何手动重置管理员密码？

在无法访问网络界面的情况下，修改密码的唯一方法是通过数据库修改。你可以使用 **pgAdmin** *(postgres)*, **DBeaver** *(mysql, mariadb)*, **SQL Management Studio** *(mssql)* 或 **DB Browser for SQLite** 等数据库管理工具。

连接到您的数据库，进入`users`表并找到要修改的用户。

修改`password`项并插入一个**bcrypt**格式的值。你可以使用 https://bcrypt-generator.com/ 这样的工具来生成这个值。加密轮数须设定为 **12**。

> **你不可能读取当前的明文密码。** 密码是经过单向bcrypt哈希后存储的，这是不可逆的。只能用新值覆盖它。
{.is-warning}

### 如果你是docker用户

如果你的PostgreSQL是在docker镜像中运行的话（如：DigitalOcean/AWS官方镜像），你可以执行如下操作：

1. 使用 https://bcrypt-generator.com/ 这样的工具来生成你想要的新密码，加密轮数须设定为 **12**。
2. 通过SSH连接到您的服务器。
3. 将下面指令中的`HASH-PASSWORD`改为您在第1步生成的值，`YOUR-EMAIL`改为你想要重置密码的账户的电子邮件地址，并执行。

```bash
docker exec db psql -U wiki -d wiki -c "UPDATE users SET password = 'HASH-PASSWORD' WHERE email = 'YOUR-EMAIL';"
```

# 电子邮件中的链接不正确

**原因**: 你还没有在 **管理区** 中设定 `站点地址`。

**解决方案**: 在 **管理区** 中的 **基本设置**下, 设定 **站点地址**.

# MySQL - Client does not support authentication protocol requested by server; consider upgrading MySQL client

**原因**: 用于让Wiki.js连接到数据库的数据库用户必须使用`mysql_native_password`。 更新的 `caching_sha2_password`方法在MySQL 8.0之后才被引入，且还未被Node.js支持。Wiki.js将在Node.js数据库驱动提供相关支持后支持这个方法。

**解决方案**: 你可以使用如下语句将对应用户的密码认证方法改为 `mysql_native_password`:

```sql
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
```

# 某些HTML标签被渲染为纯文本

从**2.1**版本开始，渲染流程中新增了HTML净化步骤。加入这一功能是为了避免潜在的不安全HTML标签/属性出现在最终渲染的页面中。任何不在白名单内的HTML标签或属性都将被以纯文本格式渲染。

如果您是wiki中唯一的编辑者/信任您的编辑团队，您可以在**管理区**的 **渲染** > **HTML** > **安全** > **净化HTML**中禁用此功能。

# 无法从管理区升级

如果点击<kbd>执行升级</kbd>按钮无法升级wiki实例，您需要把 wiki-update-companion 镜像更新到最新版本。之前的某个版本存在无法拉去最新镜像的bug。


如果你正在使用[DigitalOcean Wiki,js实例](/install/digitalocean)或根据[Ubuntu系统下安装指南](/install/ubuntu)安装的Wiki.js，您可以通过SSH连接到您的服务器，并执行以下指令：

```
docker stop wiki-update-companion
docker rm wiki-update-companion
docker pull ghcr.io/requarks/wiki-update-companion:latest
docker create --name=wiki-update-companion -v /var/run/docker.sock:/var/run/docker.sock:ro --restart=unless-stopped -h wiki-update-companion --network=wikinet ghcr.io/requarks/wiki-update-companion:latest
docker start wiki-update-companion
```

<kbd>执行升级</kbd>按钮应该就恢复正常工作了。

![](https://a.icons8.com/IMfhdRiW/YNcdYW/svg.svg){.align-abstopright}