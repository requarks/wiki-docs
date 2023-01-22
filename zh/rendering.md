---
title: 渲染流程
description: 控制您的内容的渲染方式
published: true
date: 2023-01-22T10:09:19.120Z
tags: 
editor: markdown
dateCreated: 2023-01-08T10:33:45.162Z
---

# 概述

渲染流程规定了您的内容是如何被渲染为最终呈现的可读形式的。

渲染模块隶属于核心语言模块。根据使用的编辑器的不同，内容将经过几个**核心渲染模块（Core rendering module, <kbd>CRM</kbd>）** 的处理。例如：使用Markdown编辑器的内容将经过Markdown CRM的处理，然后再被HTML CRM处理。

每个核心渲染模块可由数个**拓展渲染模块（extension rendering module, <kbd>ERM</kbd>）** 组成。这些模块拓展了核心渲染模块的能力。

![渲染流水线图示](/assets/diagrams/diag-rendering-pipeline.jpg =1000x){.radius-7 .decor-shadow}

每个模块都可以被单独启用/停用，并通过 **管理区** 菜单栏的 **渲染** 项进行配置。

# Markdown
## Tabset {.tabset}
### 定义
将Markdown内容转换为HTML。

### 参数
- **允许 HTML**: 允许转换内容中的HTML标签。
- **自动转换链接**: 链接将被自动转换为可点击的形式。
- **自动转换换行符**: 在段落之间添加换行符。
- **样式修正**: 进行一些语言中立性质的替换和引用美化。
- **引用样式**: 当样式修正启用时，单/双引号替换对。When typographer is enabled. Double + single quotes replacement pairs. e.g. «»„“ for Russian, „“‚‘ for German, etc.
> 译者并不理解**引用样式**参数的描述，在此保留原文供读者自行判断。欢迎通过issue或pull request等进行修正。
{.is-warning}

{.grid-list}


## 缩写
### Tabset {.tabset}
#### 定义
将缩写词转换为`<abbr>`标签以方便进一步解释。

#### 示例
```
*[HTML]: 超文本标记语言
*[W3C]:  万维网联盟
HTML规范由W3C维护。
```
将被渲染为

```html
<p><abbr title="超文本标记语言">HTML</abbr> 规范由<abbr title="万维网联盟">W3C</abbr>维护。</p>
```

#### 参数
*该模块不含任何可供配置的参数。*


## Emoji
### Tabset {.tabset}
#### 定义
将特定标签转为emoji。

#### 示例
 `:apple:` 将被转换为 :apple:

#### 参数
*该模块不含任何可供配置的参数。*


## 拓展制表符
### Tabset {.tabset}
#### 定义
自动将制表符转换为空格，以确保HTML中的缩进间距一致。

#### 参数
- **制表符宽度**: 转换为制表符时每个制表符对应的空格符数量。
{.grid-list}


## 脚注
### Tabset {.tabset}
#### 定义
生成脚注规范。

#### 示例
参见 https://github.com/markdown-it/markdown-it-footnote

#### 参数
*该模块不含任何可供配置的参数。*


## 图片大小
### Tabset {.tabset}
#### 定义
向图片标签添加图片大小参数。

#### 示例
```
![测试](image.png =100x200)
```
将被渲染为
```html
<p><img src="image.png" alt="test" width="100" height="200"></p>
```

#### 参数
*该模块不含任何可供配置的参数。*


## Katex
### Tabset {.tabset}
#### 定义
使用KaTeX引擎从TeX表达式生成可视化的数学/化学表达式。

> 此模块与**Mathjax**模块不兼容。一次只能启用其中一个。
{.is-danger}

#### 参数
- **行内TeX语句识别**: 处理由$符号包围的行内TeX表达式。
- **TeX区块识别**: 处理由$$符号包围的TeX块。
{.grid-list}


## Kroki
### Tabset {.tabset}
#### 定义
根据各种文本描述生成图表。

图表类型必须放在第二行，且须为小写。
您可以查阅 https://kroki.io/#support 获取支持的图表类型的完整列表。

> 该模块只在**2.4 及以上版本**可用。
{.is-info}

#### 示例
````markdown
```kroki
mermaid

graph TD
  A[ 任何人 ] -->|都可以帮助 | B( 到 github.com/yuzutech/kroki )
  B --> C{ 如何贡献？ }
  C --> D[ 报告Bug ]
  C --> E[ 分享想法 ]
  C --> F[ 推广 ]
```
````

#### Parameters
- **Kroki服务端**: 用于生成图片的Kroki服务端
- **开头标记**: 用作开头分隔符的字符串。图表类型必须以小写形式放在下一行。
- **结尾标记**: 用作结束分隔符的字符串。
{.grid-list}


## Mathjax
### Tabset {.tabset}
#### 定义
使用Mathjax引擎从TeX表达式生成可视化的Math/Chemical表达式。

> 此模块与**Katex**模块不兼容。一次只能启用其中一个。
{.is-danger}

> 该模块只在**2.4 及以上版本**可用。
{.is-info}

#### 参数
- **行内TeX语句识别**: 处理由$符号包围的行内TeX表达式。
- **TeX区块识别**: 处理由$$符号包围的TeX块。
{.grid-list}


## PlantUML
### Tabset {.tabset}
#### 定义
根据PlantUML描述生成图表。

#### 参数
- **PlantUML 服务端**: 用于生成图表的PlantUML服务端。
- **开头标记**: 用作开头分隔符的字符串。
- **结尾标记**: 用作结束分隔符的字符串。
- **图片格式**: PlantUML图标要被渲染成的格式。
{.grid-list}


## 下标/上标
### Tabset {.tabset}
#### 定义
将文本转换为下标或上标标签。

#### 示例
```
H~2~0
Exp^10^
```
将被渲染为
```html
H<sub>2</sub>O
Exp<sup>10</sup>
```

#### 参数
- **下标**: 启用下标标签。
- **上标**: 启用上标标签。
{.grid-list}


## 任务列表
### Tabset {.tabset}
#### 定义
将方括号列表转换为HTML复选框。

#### 示例
```
- [ ] 列表项 1
- [ ] 列表项 2
- [x] 列表项 3
```
将被渲染为

- [ ] 列表项 1
- [ ] 列表项 2
- [x] 列表项 3

#### 参数
*该模块不含任何可供配置的参数。*


# HTML
### Tabset {.tabset}
#### 定义
通过拓展模块处理HTML。

#### 参数
- **将相对路径视为绝对路径**: 例如，在xyz页面指向foo/bar的链接将被渲染为/foo/bar而不是/xyz/foo/bar。
- **在新标签页打开外链**: 外链将被自动添加_blank目标属性。
- **打开_blank目标链接时防止XSS**: 具有_blank属性的外链将被自动添加额外的rel属性。
{.grid-list}


## Asciinema
*即将上线*


## 引用区块
### Tabset {.tabset}
#### 定义
解析引用区块样式。

#### 示例
参见 https://docs.requarks.io/en/editors/markdown#blockquotes

#### 参数
*该模块不含任何可供配置的参数。*


## 代码高亮后处理
### Tabset {.tabset}
#### 定义
自动检测编程代码的语法并应用正确的代码着色类。

#### 参数
*该模块不含任何可供配置的参数。*


## 媒体播放器
*即将上线*


## Mermaid
### Tabset {.tabset}
#### 定义
将Mermaid代码区块转换为Mermaid图表。

> 该模块只在**2.3 及以上版本**可用。
{.is-info}

#### 参数
*该模块不含任何可供配置的参数。*


## 安全
### Tabset {.tabset}
#### 定义
过滤并去除具有潜在危险的内容。

#### 参数
- **清理 HTML**: 清除HTML中可能导致XSS攻击的不安全属性和标记。
- **允许 iframes**: 如果启用，则渲染时不会删除iframe。 *（不推荐）*
{.grid-list}


## 选项卡
### Tabset {.tabset}
#### 定义
创建选项卡以组织内容。

> 该模块只在**2.4 及以上版本**可用。
{.is-info}

#### 示例
参见 https://docs.requarks.io/en/editors/markdown#content-tabs

#### 参数
*该模块不含任何可供配置的参数。*


## Twemoji
### Tabset {.tabset}
#### 定义
将 emojis 转换为对应的 Twemoji。*(Twitter设计的emoji)*.

#### 参数
*该模块不含任何可供配置的参数。*
