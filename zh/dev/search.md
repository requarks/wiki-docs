---
title: Search Engine
description: Developing search engine modules
published: true
date: 2019-03-08T03:53:41.212Z
tags: 
---

A search engine module connects Wiki.js with an external search engine to perform page search and word suggestion queries. It consists of properties that can be set by the user as well as methods that are called on certain events, such as to create, update and delete content.

Search engine modules are located in `/server/modules/search`.

A unique folder is created for each module. The folder contains two files:

- **definition.yml**
- **storage.js**

## definition.yml

This file contains information about your module.

```yaml
key: example
title: Example Search Engine
author: John Doe
props:
  firstExampleProperty: String
  secondExampleProperty: Number
```

### Properties

* **key**: A short, unique and camelCase-formatted name for this module. It must match exactly the module folder name!
* **title**: The full name of the module.
* **author**: The name of the author of the module.
* **props**: An object of user editable properties. See [Module Properties](/dev/module-properties) for more info.

## engine.js

This file contains methods that will be called for a search query and when a new page is created, modified, deleted, etc.

```javascript
module.exports = {
  async activated () {

  },
  async deactivated () {

  },
  async init () {
  
  },
  async suggest (q, opts) {
  
  },
  async query (q, opts) {
  
  },
  async created (page) {

  },
  async updated (page) {

  },
  async deleted (page) {

  },
  async renamed (page) {

  },
  async rebuild () {
  
  }
}
```