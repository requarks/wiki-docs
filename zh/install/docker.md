---
title: Docker
description: Docker映像入门
published: true
date: 2023-03-16T08:45:000Z
tags: setup, docker, 安装
editor: markdown
dateCreated: 2023-01-08T10:35:58.261Z
---

> 在继续之前，请确保您满足[系统要求](/install/requirements)。
{.is-info}

# 使用Docker映像

Wiki.js在GitHub Packages上以`ghcr.io/reqarks/wiki`发布Docker映像，在Docker Hub上以`reqarks/wiki`的形式发布。

> 强烈建议您不要使用`latest`标签，而是使用所需的主要版本，例如`ghcr.io/reqarks/wiki:2`
>
> 您也可以将映像指向特定的次要版本（例如`ghcr.io/remarks/wiki:2.5`），尽管在拉取映像时不会自动获得最新功能。
{.is-info}

- 在[GitHub Packages](https://github.com/Requarks/wiki/pkgs/container/wiki)查看
- 在[Docker Hub](https://hub.docker.com/r/requarks/wiki)查看

## 环境变量
必须设置以下环境变量。除非另有规定，否则均为**必需**。

### 数据库

- **DB_TYPE** : 数据库类型 (`mysql`, `postgres`, `mariadb`, `mssql` 或 `sqlite`)
{.grid-list}

*以下仅适用于PostgreSQL, MySQL, MariaDB 和 MSSQL:*

- **DB_HOST** : 数据库主机名或IP
- **DB_PORT** : 数据库端口
- **DB_USER** : 连接到数据库的用户名
- **DB_PASS** : 连接到数据库的密码
- **DB_NAME** : 数据库名称
{.grid-list}

*当要连接到强制要求SSL连接的数据库时:*

- **DB_SSL** : 设为 `1` 或 `true` 以启用。 *(可选，如果省略则默认关闭)*
- **DB_SSL_CA** : 数据库CA证书内容，作为单行字符串（不带空格或结尾空白行），不带前缀和后缀行。*(可选，需要2.3及以上版本)*
{.grid-list}

*通过本地文件secret提供数据库密码的另一种方法:*

- **DB_PASS_FILE**: 包含数据库密码的映射文件的路径。 *(可选，代替DB_PASS变量)*
{.grid-list}

*仅适用于SQLite:*

- **DB_FILEPATH** : SQLite文件的路径
{.grid-list}

### HTTPS

> 此功能只在**2.1及以上版本可用**
{.is-info}

Wiki.js提供了环境变量以方便Let's Encrypt配置。
如果要提供自己的SSL证书配置，则必须[按下面的说明](#alternative-mount-the-config-file)挂载配置文件。

- **SSL_ACTIVE** : 设为 `1` 或 `true` 以启用。 *(可选，如果省略则默认关闭)*
- **LETSENCRYPT_DOMAIN** : 从Let's Encrypt请求证书时使用的域/子域（例如“wiki.example.com”）
- **LETSENCRYPT_EMAIL** : 从Let's Encrypt请求证书时使用的管理员电子邮件。
{.grid-list}

暴露的HTTPS端口为`3443`。使用Let's Encrypt时，必须开放HTTP和HTTPS端口。

> **HTTP端口必须可从internet访问，证书设置才能完成！**
> 生成证书后，您可以从**管理区**的**SSL**部分下启用自动HTTPS重定向。
> 
> 请注意，为了使证书续订过程正常工作，必须始终保持HTTP端口打开并可访问。启用上述选项（HTTPS重定向）时，这**不是**安全风险。
{.is-warning}

### 高可用

> 此功能只在**2.3及以上版本可用**
{.is-info}

当使用多个副本（例如Kubernetes cluster/Docker Swarm）运行Wiki.js时，必须启用高可用，以确保将任何更改传播到其他实例。

- **HA_ACTIVE** : 设为 `1` 或 `true` 以启用。 *(可选，如果省略则默认关闭)*
{.grid-list}

> 您必须使用**PostgreSQL**数据库才能启用此功能。它不能与任何其他数据库引擎一起工作！
{.is-warning}

## 示例

下面是一个运行Wiki.js连接到PostgreSQL数据库的命令示例：
```bash
docker run -d -p 8080:3000 --name wiki --restart unless-stopped -e "DB_TYPE=postgres" -e "DB_HOST=db" -e "DB_PORT=5432" -e "DB_USER=wikijs" -e "DB_PASS=wikijsrocks" -e "DB_NAME=wiki" ghcr.io/requarks/wiki:2
```

连接到MySQL的示例：
```bash
docker run -d -p 8080:3000 --name wiki --restart unless-stopped -e "DB_TYPE=mysql" -e "DB_HOST=db" -e "DB_PORT=3306" -e "DB_USER=wikijs" -e "DB_PASS=wikijsrocks" -e "DB_NAME=wiki" ghcr.io/requarks/wiki:2
```

> 这两个示例都假设在同一网络上的另一个名为“db”的容器中运行数据库。
> Wiki.js**没有**附带数据库引擎。有关详细信息，请参阅[安装要求]（/install/requirements）。
{.is-warning}

Let's Encrypt 示例:
```bash
docker run -d -p 80:3000 -p 443:3443 -e "LETSENCRYPT_DOMAIN=wiki.example.com" -e "LETSENCRYPT_EMAIL=admin@example.com" --name wiki --restart unless-stopped -e "DB_TYPE=postgres" -e "DB_HOST=db" -e "DB_PORT=5432" -e "DB_USER=wikijs" -e "DB_PASS=wikijsrocks" -e "DB_NAME=wiki" ghcr.io/requarks/wiki:2
```

## 备选方案：挂载配置文件

如果你不喜欢使用环境变量，你也可以挂载一个配置文件。

根据[示例配置文件](https://github.com/Requarks/wiki/blob/master/config.sample.yml)创建一个新文件，并修改值以匹配您的设置。然后可以在容器中挂载配置文件：

```bash
docker run -d -p 8080:3000 --name wiki --restart unless-stopped -v YOUR-FILE.yml:/wiki/config.yml ghcr.io/requarks/wiki:2
```

还可以使用 CONFIG_FILE 环境变量为要从中加载的配置文件定义另一个位置。这在您希望呱噪配置文件夹的情况下非常有用。

- **CONFIG_FILE** : config.yml文件的路径
{.grid-list}

## 更改用户

默认情况下，Wiki.js以用户`wiki`的身份运行。如果在装载文件（如SQLite 数据库或私钥）时遇到权限问题，可以使用`-u`参数重写运行时用户以`root`身份运行，例如：

```bash
docker run -d -p 8080:3000 -u="root" --name wiki --restart unless-stopped -e "DB_TYPE=postgres" -e "DB_HOST=db" -e "DB_PORT=5432" -e "DB_USER=wikijs" -e "DB_PASS=wikijsrocks" -e "DB_NAME=wiki" ghcr.io/requarks/wiki:2
```

然而，这不是运行容器的安全方法。在这样做之前，请确保您了解安全影响。

# 使用 Docker Compose

下面是一个完整的Wiki.js Docker Compose文件示例，使用PostgreSQL，监听端口80：

```yaml
version: "3"
services:

  db:
    image: postgres:11-alpine
    environment:
      POSTGRES_DB: wiki
      POSTGRES_PASSWORD: wikijsrocks
      POSTGRES_USER: wikijs
    logging:
      driver: "none"
    restart: unless-stopped
    volumes:
      - db-data:/var/lib/postgresql/data

  wiki:
    image: ghcr.io/requarks/wiki:2
    depends_on:
      - db
    environment:
      DB_TYPE: postgres
      DB_HOST: db
      DB_PORT: 5432
      DB_USER: wikijs
      DB_PASS: wikijsrocks
      DB_NAME: wiki
    restart: unless-stopped
    ports:
      - "80:3000"

volumes:
  db-data:
```

![](https://a.icons8.com/jihZbhdR/4WJoF7/svg.svg){.align-abstopright}

# ARM 映像

> 自**2.4版本**起，ARMv7和ARM64图像与AMD64是同一docker映像标签的一部分。只需使用与上述相同的标签。
{.is-info}

此映像兼容：

- **ARM64**: 树莓派4，3和更高版本树莓派2（v1.2）
- **ARMv7**: 早期版本的树莓派2（v1.1）

最初的第一代树莓派**不受支持** *（ARMv6）*。

# OpenShift

[此处](https://github.com/Requarks/wiki/blob/master/dev/openshift/Dockerfile)提供了一个与OpenShift兼容的Dockerfile示例。
