---
title: Comments
description: Developer guide for Commenting modules
published: true
date: 2020-05-16T20:05:17.187Z
tags: 
---

> Available from version **2.4 and up**
{.is-info}

An comments module adds discussion capabitilies to your wiki. It consists of properties that can be set by the user as well as methods that are called on certain events \(e.g. posting a new comment\).

Comments modules are located in `/server/modules/comments`.

There're 2 supported formats for comments modules:

- **Code Templates**: External services where you embed an HTML / JS code in your page to display the comments. (e.g. Disqus)
- **Native**: Use Wiki.js UI to display and post comments. Comments are processed server-side.

A unique folder is created for each module. The folder must contains these files:

* **definition.yml**
* **code.yml** *(Code Template only)*
* **comment.js** *(Native only)*

## definition.yml

This file contains information about your module.
```yaml
key: example
title: Example Comments Provider
author: John Doe
logo: https://static.requarks.io/logo/example.svg
website: https://example.com/
codeTemplate: true
isAvailable: true
props:
  firstExampleProperty: String
  secondExampleProperty: Number
```

### Properties

* **key**: A short, unique and camelCase-formatted name for this module. It must match exactly the module folder name!
* **title**: The full name of the module.
* **author**: The name of the author of the module.
* **logo**: The URL to the module logo.
* **website**: The URL to the module website / developer website.
* **codeTemplate**: Whether to use Code Template format (`true`) or native (`false`)
* **isAvailable**: Whether the user can use the module or not.
* **props**: An object of user editable properties. See [Module Properties](/dev/module-properties) for more info.

## code.yml

This file contains the code snippets to inject into the head, body and comment slot.

```yaml
main: |
  <div id="external_thread"></div>
body: |
  <script>
    var something = remote()
  </script>
```

### Properties

* **main**: The HTML code snippet where the comments will be displayed. *(Required, HTML only)*
* **head**: The HTML code snippet to inject in the page head. *(Optional, JS and CSS only)*
* **body**: The HTML code snippet to inject at the end of the page body. *(Optional, JS and CSS only)*

## comment.js

This file contains methods that will be called on specific events.

```js
/* global WIKI */

// ------------------------------------
// Example Comments Provider
// ------------------------------------

const ExampleStrategy = require('example')

module.exports = {
  add (args) {
    // Code here to add a comment
  }
}
```

All methods are required and must be implemented.

### add

Upon initialization of Wiki.js \(both startups or restarts\).

```js
add (args) { }
```

Parameter **args** is... TODO
