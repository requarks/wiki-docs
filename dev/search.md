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
- **engine.js**

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
  async activate () {

  },
  async deactivate () {

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

### Tips

#### Query requires specific schema

Query is the only one which has a different schema because its piped directly into the graphql api. 
The changes you need to make is localeCode needs to be locale and instead of returning pages, you need to return an object matching:

```javascript
{
  suggestions: [],
  results: []
  totalHits: 0
}
```

Where suggestions, this is a string array like search suggestions.
Where results, these are the pages with the mutated localeCode to locale.
Where totalHits, change this to be a length of results.

#### Getting Content from the Database

Models such as pages are accessed through knex, an example of how you could query all pages to do something like rebuild is:

```javasript
const stream = WIKI.models.knex
  .column(
    { id: "hash" },
    "path",
    "title",
    "description",
    "hash",
    "isPrivate",
    "isPublished",
    "content",
    "contentType",
    "createdAt",
    "updatedAt",
    "editorKey",
    "authorId",
    "creatorId",
    "localeCode",
    { realId: "id" },
  )
  .select()
  .from("pages")
  .where({
    isPublished: true,
    isPrivate: false,
  })
  .stream();
```

#### Logging

Logging is already setup and available in wikijs, to access it try using the code below:

```javascript
/**
 * @type {Console}
 */
let logger = WIKI.logger;
```
