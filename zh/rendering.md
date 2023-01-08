---
title: Rendering Pipeline
description: Control how your content is rendered
published: true
date: 2020-05-23T05:16:48.570Z
tags: 
---

# Overview

The rendering pipeline defines how your content is rendered into it's final readable form.

Rendering modules are attached to a core language module. Depending on the editor used, content will go through several **core rendering modules <kbd>CRM</kbd>**. For example, using the Markdown editor will result in the content being transformed through the Markdown CRM, then by the HTML CRM modules.

Each core rendering module can consists of multiple **extension rendering modules <kbd>ERM</kbd>**. These modules extend the capabilities of the core rendering module.

![Rendering Pipeline Diagram](/assets/diagrams/diag-rendering-pipeline.jpg =1000x){.radius-7 .decor-shadow}

Each module can be enabled / disabled individually and configured in the **Administration Area** under the **Rendering** sidebar menu.

# Markdown
## Tabset {.tabset}
### Definition
Converts Markdown content into HTML.

### Parameters
- **Allow HTML**: Enable HTML tabs in content.
- **Automatically convert links**: Links will automatically be converted into clickable links.
- **Automatically convert line breaks**: Add linebreaks within paragraphs.
- **Typographer**: Enable some language-neutral replacement + quotes beautification.
- **Quotes style**: When typographer is enabled. Double + single quotes replacement pairs. e.g. «»„“ for Russian, „“‚‘ for German, etc.
{.grid-list}


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
Convert tags into emojis.

#### Example
 `:apple:` will produce :apple:

#### Parameters
*This module doesn't have any configurable parameters.*


## Expand Tabs
### Tabset {.tabset}
#### Definition
Automatically convert tabs into spaces for consistent indentation spacing in HTML.

#### Parameters
- **Tab Width**: The number of spaces to use when converting from tabs.
{.grid-list}


## Footnotes
### Tabset {.tabset}
#### Definition
Generates footnote definitions.

#### Example
See https://github.com/markdown-it/markdown-it-footnote

#### Parameters
*This module doesn't have any configurable parameters.*


## Image Size
### Tabset {.tabset}
#### Definition

Add image dimensions to img tags.

#### Example
```
![test](image.png =100x200)
```
will result in
```html
<p><img src="image.png" alt="test" width="100" height="200"></p>
```

#### Parameters
*This module doesn't have any configurable parameters.*


## Katex
### Tabset {.tabset}
#### Definition
Generate visual Math / Chemical expressions from TeX expressions, using the KaTeX engine.

> This module is incompatible with the **Mathjax** module. Only one of them should be enabled at once.
{.is-danger}

#### Parameters
- **Inline TeX**: Process inline TeX expressions surrounded by $ symbols.
- **TeX Blocks**: Process TeX blocks enclosed by $$ symbols.
{.grid-list}


## Kroki
### Tabset {.tabset}
#### Definition
Generate diagrams from various textual descriptions.

The diagram type must be put on the second line, in lowercase.
See https://kroki.io/#support for the full list of supported diagram types.

> This module is only available from version **2.4 and up**.
{.is-info}

#### Example
````markdown
```kroki
mermaid

graph TD
  A[ Anyone ] -->|Can help | B( Go to github.com/yuzutech/kroki )
  B --> C{ How to contribute? }
  C --> D[ Reporting bugs ]
  C --> E[ Sharing ideas ]
  C --> F[ Advocating ]
```
````

#### Parameters
- **Kroki Server**: Kroki server used for image generation
- **Open Marker**: String to use as opening delimiter. Diagram type must be put in the next line in lowercase.
- **Close Marker**: String to use as closing delimiter
{.grid-list}


## Mathjax
### Tabset {.tabset}
#### Definition
Generate visual Math / Chemical expressions from TeX expressions, using the Mathjax engine.

> This module is incompatible with the **Katex** module. Only one of them should be enabled at once.
{.is-danger}

> This module is only available from version **2.4 and up**.
{.is-info}

#### Parameters
- **Inline TeX**: Process inline TeX expressions surrounded by $ symbols.
- **TeX Blocks**: Process TeX blocks enclosed by $$ symbols.
{.grid-list}


## PlantUML
### Tabset {.tabset}
#### Definition
Generate diagrams from PlantUML description.

#### Parameters
- **Kroki Server**: PlantUML server used for image generation.
- **Open Marker**: String to use as opening delimiter.
- **Close Marker**: String to use as closing delimiter.
- **Image Format**: Format to use for rendered PlantUML images
{.grid-list}


## Subscript/Superscript
### Tabset {.tabset}
#### Definition
Transform text into subscript and superscript tags.

#### Example
```
H~2~0
Exp^10^
```
will result in
```html
H<sub>2</sub>O
Exp<sup>10</sup>
```

#### Parameters
- **Subscript**: Enable subscript tags.
- **Superscript**: Enable supercript tags
{.grid-list}


## Task Lists
### Tabset {.tabset}
#### Definition
Convert square brackets list into HTML checkboxes.

#### Example
```
- [ ] Item 1
- [ ] Item 2
- [x] Item 3
```
will result in

- [ ] Item 1
- [ ] Item 2
- [x] Item 3

#### Parameters
*This module doesn't have any configurable parameters.*


# HTML
### Tabset {.tabset}
#### Definition
Process HTML through extension modules.

#### Parameters
- **Treat relative links as root absolute**: For example, a link to foo/bar on page xyz will render as /foo/bar instead of /xyz/foo/bar.
- **Open external links in a new tab**: External links will have a _blank target attribute added automatically.
- **Protect against XSS when opening _blank target links**: External links with _blank attribute will have an additional rel attribute.
{.grid-list}


## Asciinema
*Coming soon*


## Blockquotes
### Tabset {.tabset}
#### Definition
Parse blockquotes box styling.

#### Example
See https://docs.requarks.io/en/editors/markdown#blockquotes

#### Parameters
*This module doesn't have any configurable parameters.*


## Code Highlighting Post-Processor
### Tabset {.tabset}
#### Definition
Automatically detect programming code syntax and apply the correct code coloring classes.

#### Parameters
*This module doesn't have any configurable parameters.*


## Media Players
*Coming soon*


## Mermaid
### Tabset {.tabset}
#### Definition
Transform Mermaid code blocks into Mermaid diagrams.

> This module is only available from version **2.3 and up**.
{.is-info}

#### Parameters
*This module doesn't have any configurable parameters.*


## Security
### Tabset {.tabset}
#### Definition
Filter and strip potentially dangerous content.

#### Parameters
- **Sanitize HTML**: Sanitize HTML from unsafe attributes and tags that could lead to XSS attacks.
- **Allow iframes**: iframes will not be stripped if enabled. *(Not recommended)*
{.grid-list}


## Tabsets
### Tabset {.tabset}
#### Definition
Create tabs to organize content.

> This module is only available from version **2.4 and up**.
{.is-info}

#### Example
See https://docs.requarks.io/en/editors/markdown#content-tabs

#### Parameters
*This module doesn't have any configurable parameters.*


## Twemoji
### Tabset {.tabset}
#### Definition
Convert emojis into their Twemoji equivalent *(Twitter emoji design)*.

#### Parameters
*This module doesn't have any configurable parameters.*
