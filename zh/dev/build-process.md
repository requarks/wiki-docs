---
title: 构建流程
description: Wiki.js的可复现构建流程
published: true
date: 2023-03-16T08:45:000Z
tags: 
editor: markdown
dateCreated: 2023-01-08T10:34:53.861Z
---

# 构建与部署工作流

所有构建均通过Azure DevOps完成，可[在线查看](https://dev.azure.com/requarks/wiki/_build?definitionId=9).

每次提交都会生成一个新版，并递增一次构建版本号 *(大版本.小版本.构建版本)*

以下文档用于了解构建如何生成，不是用于生产用途的部署方法。请使用[在此文档链接中已详细说明的](/install)预购键包/镜像。

# 构建过程

## 任务 1 - 禁用开发标识

使用**命令行**任务：

```bash
sudo apt-get install jq -y
mv package.json pkg-temp.json
jq -r '.dev |= false' pkg-temp.json > package.json
rm pkg-temp.json
```

## 任务 2 - 设定构建版本

使用[Version JSON文件](https://github.com/rfennell/AzurePipelines/wiki/Version-Assemblies-and-Packages-Tasks) 任务, 在`package.json`的`version`字段插入`$(Build.BuildNumber)`值。

## 任务 3 - 构建资源
使用**Docker**任务, 构建并推送 `requarks/wiki` 镜像, 使用`dev/build/Dockerfile`附加`canary` 标签

## 任务 4 - 提取已编译的资源

使用**命令行**任务：


```bash
docker create --name wiki requarks/wiki:canary
docker cp wiki:/wiki $(Build.StagingDirectory)
docker rm wiki
rm $(Build.StagingDirectory)/wiki/config.yml
rm $(Build.StagingDirectory)/wiki/wait.sh
cp $(System.DefaultWorkingDirectory)/config.sample.yml $(Build.StagingDirectory)/wiki/config.sample.yml
find $(Build.StagingDirectory)/wiki/ -printf "%P\n" | tar -czf wiki-js.tar.gz --no-recursion -C $(Build.StagingDirectory)/wiki/ -T -
```

## 任务 5 - 发布构建产物

使用 **发布构建产物** 任务, 将`wiki-js.tar.gz`作为产物 `drop` 至 Azure 流水线。

# 发布过程

选择最新版本发布后，将在Azure DevOps中执行以下步骤：

## BETA

```bash
docker pull requarks/wiki:canary
docker tag requarks/wiki:canary requarks/wiki:beta
docker push requarks/wiki:beta
```

构建好的产物使用关联的源版本+标记发布为GitHub版本。自动列出自上次发布以来的所有提交，作为更新日志。作为**预发布**版本。

来自构建产物的如下资源被添加到此次发布的版本中：
```
$(System.DefaultWorkingDirectory)/_build/drop/*.tar.gz
$(System.DefaultWorkingDirectory)/_build/drop-win/*.tar.gz
```

完成后，释出管道关闭，等待手动批准。

## GA

```bash
docker pull requarks/wiki:beta

curl -LJO https://static.requarks.io/semver
chmod +x semver

MAJOR=`./semver get major $(Build.BuildNumber)`
MINOR=`./semver get minor $(Build.BuildNumber)`
MAJORMINOR="$MAJOR.$MINOR"

echo "Using major $MAJOR and minor $MINOR..."

docker tag requarks/wiki:beta requarks/wiki:$(Build.BuildNumber)
docker tag requarks/wiki:beta requarks/wiki:$MAJOR
docker tag requarks/wiki:beta requarks/wiki:$MAJORMINOR
docker tag requarks/wiki:beta requarks/wiki:latest

docker push requarks/wiki:$(Build.BuildNumber)
docker push requarks/wiki:$MAJOR
docker push requarks/wiki:$MAJORMINOR
docker push requarks/wiki:latest
```

GitHub版本同时被修改，删除预发布标志。
