---
title: 翻译
description: 贡献新语言或测试新语言键
published: true
date: 2023-02-06T03:24:52.240Z
tags: dev, localization, 本地化, 开发
editor: markdown
dateCreated: 2023-01-08T10:35:17.685Z
---

# 贡献新/现有语言

我们一直在寻找翻译贡献者，以使Wiki.js支持尽可能多的语言！

您可以加入下面的Lokalise项目以获取翻译工具。无需编写代码！如果您有任何问题，请随时在[Slack](https://wiki.requarks.io/slack)上与我们联系！

> **请只选择您将会积极参与贡献的语言！** 同时选择过多或所有语言的用户将被删除。
{.is-warning}

[![btn-join-the-project.png](/assets/buttons/btn-join-the-project.png)](https://lokalise.com/public/2994254859f751ea605a00.03473540/)

如果您在列表中找不到您的语言，请在[Slack](https://wiki.requarks.io/slack)上与我们联系，我们会添加这个语言！

# 查看wiki上的最新更改

对翻译所做的更改在您wiki中出现之前，需要途径各种缓存层：

- Reguarks GraphQL服务端**每5分钟**缓存一次翻译。
- 您的wiki实例**每24小时**从Requarks GraphQL服务端获取一次更改。
- 如果您使用离线侧载， [语言文件](https://github.com/Requarks/wiki-localization) 将在每天**东部标准时间（EST）上午12：00**更新。

您可以通过重新启动Wiki.js实例强制立即获取更改。获取新翻译的job将在初始化后立即启动。*请注意，您需要等待Reguarks GraphQL服务端的5分钟缓存过期后才能看到更改。*

> **浏览器缓存**
>
> 翻译在浏览器缓存中保存24小时。尽管Wiki.js实例可能有最新的更改，但在浏览器缓存过期之前，您将无法看到这些更改。您可在  **管理区** > **其它** > **刷新缓存** > **刷新客户端语言缓存**.
{.is-info}

# 如何选择贡献的翻译版本

由于多个用户可以贡献同一种语言，因此使用以下过程来选择翻译版本：

- 使用投票最多的翻译版本。
- 否则，使用最后编辑的翻译版本。

# 开发模式

如果您需要添加新键并在开发环境中实时测试，只需在`server/locales`目录中创建一个包含要测试的值的{LANG}.yml文件即可，例如：

### en.yml
```yml
admin:
  api.title: 'API Access'
  auth.title: 'Authentication'
```

官方语言键仍将首先加载，但本地文件将覆盖所有现有键（并添加新键）。

请注意，必须重新启动Wiki.js才能加载对文件所做的任何更改，在开发模式下保存文件时会自动重启。
