---
title: Rendering Pipeline
description: Control how your content is rendered
published: true
date: 2020-05-22T20:23:47.987Z
tags: 
---

# Overview

The rendering pipeline defines how your content is rendered into it's final readable form.

# Markdown


## Abbreviations

### Tabset {.tabset}

#### Definition

Transform abbreviation words into `<abbr>` tags for an expanding definition.

#### Example

```
*[HTML]: Hyper Text Markup Language
*[W3C]:  World Wide Web Consortium
The HTML specification
is maintained by the W3C.
```
will result in

```html
<p>The <abbr title="Hyper Text Markup Language">HTML</abbr> specification
is maintained by the <abbr title="World Wide Web Consortium">W3C</abbr>.</p>
```

#### Parameters

*This module doesn't have any configurable parameters.*


## Emoji

### Tabset {.tabset}

#### Definition

Convert tags into emojis. (e.g. `:apple:` into :apple:)

#### Parameters

*This module doesn't have any configurable parameters.*


## Expand Tabs

### Tabset {.tabset}

#### Definition

Automatically convert tabs into spaces for consistent indentation spacing in HTML.

#### Parameters

- **Tab Width**: The number of spaces to use when converting from tabs.
{.grid-list}

# HTML

# OpenAPI