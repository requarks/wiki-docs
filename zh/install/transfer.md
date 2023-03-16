---
title: 在服务器之间迁移Wiki.js
description: 如何将Wiki.js迁移到新服务器
published: true
date: 2023-03-16T08:45:00.000Z
tags: 
editor: markdown
dateCreated: 2023-01-08T10:36:24.308Z
---

# 开始迁移

本指南假设您当前正在使用运行在Linux Docker上的Wiki.js2.x的PostgreSQL数据库安装，详细信息请参阅[Ubuntu上的安装指南](/install/ubuntu)。这是DigitalOcean和AWS 市场一键映像采用的默认安装方法。

> 请注意，**不能**从不同的数据库引擎 *（例如MySQL、MSSQL或SQLite）*“转换”安装。您应该手动将内容导出到磁盘，然后将其重新导入到新安装中。
{.is-danger}

# 1. 配置新服务端

***环境:** 新服务器*{.caption}

让我们从设置目标服务器开始。遵循[Ubuntu安装指南](/install/ubuntu)，直到“**访问安装向导**”步骤 *（不要执行此步骤，在启动Docker容器后立即停止）*。

现在，您应该拥有一个完全初始化的服务器，其中包含PostgreSQL数据库、Wiki.js实例和Wiki.js自动更新程序，所有这些都在Docker容器中运行。

# 2. 备份数据库

***环境:** 旧服务器*{.caption}

在之前安装的旧服务器上，进行数据库完整转储：
```bash
docker exec db pg_dump wiki -U wiki -F c > wikibackup.dump
```
> 在上面的命令中，PostgreSQL docker容器名为`db`，我们使用的是数据库名`wiki`和用户`wiki`。如果您遵循了上面“入门”部分中提到的安装指南，那么这是默认设置。
{.is-info}

这将在当前目录中创建一个新文件`wikibackup.dump`。

# 3. 迁移备份
***环境:** 旧服务器*{.caption}

现在，我们将备份文件传输到新服务器上。有几种方法可以在服务器之间复制文件，但我们将在本例中使用rsync。将下面命令中的`YOUR-NEW-SERVER-IP`替换为新服务器的IP地址。

```bash
rsync -P wikibackup.dump root@YOUR-NEW-SERVER-IP:~/wikibackup.dump
```

> 这假设您之前已将新服务器配置为接受来自旧服务器的SSH连接。为此，需要将旧服务器的公钥添加到新服务器的authorized_keys中。您可以在[此教程](https://www.digitalocean.com/community/tutorials/how-to-set-up-ssh-keys-on-ubuntu-22-04)中学习。
{.is-info}

# 4. 恢复数据库

***环境:** 新数据库*{.caption}

现在，我们准备将数据库转储还原到新数据库中。

在新服务器上，停止docker容器`wiki`：

```bash
docker stop wiki
```

将`wikibackup.dump`文件还原到新数据库中，首先删除现有的空数据库：
```bash
docker exec -it db dropdb -U wiki wiki
docker exec -it db createdb -U wiki wiki
cat ~/wikibackup.dump | docker exec -i db pg_restore -U wiki -d wiki
```

我们现在可以重新启动`wiki`容器：
```
docker start wiki
```

以上就是全部迁移过程！
