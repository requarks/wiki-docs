---
title: Code
description: Editor
published: true
date: 2020-06-09T21:58:10.931Z
tags: editors
editor: markdown
---

# Overview

The Code editor is a basic raw HTML editor.

> *It's generally not recommended to use this editor to write new content. This editor is provided as a convenience to import existing content from older systems which is only available in raw HTML.*
{.is-warning}

# User Guide

Only Wiki.js specific stylings are listed below.

## Content Tabs

### Tab {.tabset}

#### Usage

> This feature is only available from version 2.4 and up.
{.is-info}

Using headers and adding the `tabset` css class to the parent header. The parent header text will not be shown in the final result.

Note that you can use any header level, as long as the children headers are one level higher. For example, if a parent header is `<h3>`, the tabs headers must be `<h4>`. The maximum header level for a parent being `<h5>` and the children `<h6>`.

#### Code Example

```html
<h2 class="tabset">Tabs</h2>

<h3>First Tab</h3>
<p>Any content here will go into the first tab...</p>

<h3>Second Tab</h3>
<p>Any content here will go into the second tab...</p>

<h3>Third Tab</h3>
<p>Any content here will go into the third tab...</p>
```