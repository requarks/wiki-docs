---
title: AsciiDoc
description: Editor
published: true
date: 2024-11-12T23:20:00.000Z
tags: editors
editor: markdown
dateCreated: 2022-12-24T02:46:14.354Z
---

# Overview

> The AsciiDoc editor is available from version **2.5.295 and up**.
{.is-info}

AsciiDoc is a lightweight and semantic markup language primarily designed for writing technical documentation. The language can be used to produce a variety of presentation-rich output formats, all from content encoded in a concise, human-readable, plain text format.

# Usage

See the [AsciiDoc Language Documentation](https://docs.asciidoctor.org/asciidoc/latest/) for more information.

> Note that only a limited set of AsciiDoc features are supported at the moment.
{.is-warning}

# Stylings

## Admonitions

In addition to the **5** [standard types](https://docs.asciidoctor.org/asciidoc/latest/blocks/admonitions/) provided by AsciiDoc, Wiki.js extends the syntax to include the **success** blockquote from the [Markdown Editor](../markdown.md).
This extension is implemented as a [Block Processor](https://docs.asciidoctor.org/asciidoctor/latest/extensions/block-processor/) as follows:

```adoc
[Success]
Success is now.
```
