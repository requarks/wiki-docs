---
title: Editors
description: Using the various editors of Wiki.js
published: true
date: 2022-12-24T02:46:24.542Z
tags: editors
editor: markdown
dateCreated: 2019-05-22T03:11:37.479Z
---

When creating a page, you can use the editor of your choice. Some users prefer to write content in Markdown while others might prefer a more visual editor.

# List of  Editors

- [AsciiDoc *Plain Text Formatting*](/editors/asciidoc) 
- [Code *Raw HTML*](/editors/code)
- [Markdown *Plain Text Formatting*](/editors/markdown)
- [Visual Editor *Rich-Text WYSIWYG*](/editors/visualeditor)
{.links-list}

# Change Editor

> This feature is available from version **2.5.201 and up**.
{.is-info}

You can change the editor used for any page using the **Convert** action. This will attempt to convert the content to be used by the newly selected editor. For example, a page previously created with the Markdown editor can be converted to HTML to be used with the Visual Editor.

From the **Page Actions** menus (located at the top-right corner and bottom-right corner), select **Convert**. The following dialog is shown:

![ui-convert-page-dialog.png](/assets/ui/ui-convert-page-dialog.png =550x){.radius-5 .decor-shadow}

Select the editor you want to use going forward and click **Convert**.

> :warning: **Important**
>
> Because of differences between editor / format capabilities, some formatting or non-rendered content may be lost after the conversion.
>
> A snapshot of the page is **automatically taken before the conversion** and you can revert or refer to this version **at any time afterwards** from the page history.
>
> _Examples_
>
> &#8727; When going from Markdown to HTML, `draw.io` diagrams will be kept as their final rendered image. You will no longer be able to edit the diagram.
> &#8727; When going from Markdown to HTML, tabsets will be reverted to standard headers and paragraphs (as seen in the markdown editor).
> &#8727; When going from HTML to Markdown, custom CSS classes and HTML elements that don't exist in the Markdown language will not be preserved.
{.is-warning}

As a reference, the following format conversions occur based on the source / target editor selected:

| Source | Target | Format Conversion
| -- | -- | -- |
| Markdown | Visual Editor | Markdown -> HTML |
| Markdown | Raw HTML | Markdown -> HTML |
| Visual Editor | Markdown | HTML -> Markdown |
| Visual Editor | Raw HTML | *no format conversion needed*{.caption} |
| Raw HTML | Markdown | HTML -> Markdown |
| Raw HTML | Visual Editor | *no format conversion needed*{.caption} |