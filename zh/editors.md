---
title: 编辑器
description: 使用Wiki.js的多种编辑器
published: true
date: 2023-03-16T08:45:00.000Z
tags: editors, 编辑器
editor: markdown
dateCreated: 2023-01-08T10:33:24.814Z
---

创建页面时，可以使用您选择的编辑器。一些用户更喜欢用Markdown编写内容，而另一些用户可能更喜欢更直观的编辑器。

# 编辑器列表

- [AsciiDoc *纯文本格式*](/editors/asciidoc) 
- [代码 *纯HTML*](/editors/code)
- [Markdown *纯文本格式*](/editors/markdown)
- [可视编辑器 *富文本，所见即所得*](/editors/visualeditor)
{.links-list}

# 更改编辑器

> 仅在版本 **2.5.201及以上**可用。
{.is-info}

您可以使用**转换**操作更改用于任何页面的编辑器。这将使wiki尝试将内容转换至可被新编辑器使用的内容。例如，以前使用Markdown编辑器创建的页面可以转换为HTML，以便与可视化编辑器一起使用。

页面操作菜单（右上角和右下角）将显示如下对话框：

![ui-convert-page-dialog.png](/assets/ui/ui-convert-page-dialog.png =550x){.radius-5 .decor-shadow}

选择要继续使用的编辑器，然后单击**转换**。

> :warning: **重要**
>
> 由于编辑器/格式功能之间的差异，某些格式或未渲染的内容可能会在转换后丢失。
>
> 系统在**转换之前会自动抓取**页面快照，您可以在之后的任何时间从页面历史记录中还原或引用此版本。
>
> _示例_
>
> &#8727; 当从Markdown转换为HTML时，`draw.io`图表将变为其最终渲染图像保留。您将无法再编辑图表。
> &#8727; 从Markdown转换为HTML时，标签集将恢复为标准标题和段落（如Markdown编辑器中所示）。
> &#8727; 当从HTML转到Markdown时，Markdown语言中不存在的自定义CSS类和HTML元素将不会被保留。
{.is-warning}

作为参考，以下格式转换基于所选的源/目标编辑器进行：

| 源编辑器 | 目标编辑器 | 格式转换
| -- | -- | -- |
| Markdown | 可视编辑器 | Markdown -> HTML |
| Markdown | 纯HTML | Markdown -> HTML |
| 可视编辑器 | Markdown | HTML -> Markdown |
| 可视编辑器 | 纯HTML | *无需进行格式转换*{.caption} |
| 纯HTML | Markdown | HTML -> Markdown |
| 纯HTML | 可视编辑器 | *无需进行格式转换*{.caption} |