---
title: Storage
description: Developing storage modules
published: true
date: 2019-09-07T16:00:04.223Z
tags: 
---

A storage module connects Wiki.js with a local or remote storage provider, to act as backup or source of truth for content. It consists of properties that can be set by the user as well as methods that are called on certain events, such as to create, update and delete content.

Storage modules are located in `/server/modules/storage`.

A unique folder is created for each module. The folder contains two files:

* **definition.yml**
* **storage.js**

## definition.yml

This file contains information about your module.

```yaml
key: example
title: Example Storage
description: A short description about Example Storage
author: John Doe
logo: https://../example.svg
website: https://www.example.com/
isAvailable: true
supportedModes:
	- push
defaultMode: push
schedule: false
props:
  firstExampleProperty: String
  secondExampleProperty: Number
actions:
	- handler: firstAction
    label: First Action Example
    hint: Description of what this action does
```

### Properties

* **key**: A short, unique and camelCase-formatted name for this module. It must match exactly the module folder name!
* **title**: The full name of the module.
* **description**: A short description of the module.
* **author**: The name of the author of the module.
* **logo**: Absolute URL to the logo of the module provider. An SVG vector is required.
* **website**: URL to the website of the module provider.
* **isAvailable**: Whether the module can be activated / configured by the administrator.
* **supportedModes**: A list of supported modes. Unless your module specifically supports bi-directional sync, only the `push` option should be listed. Possible values:
	* `sync`: Content is first pulled from the storage target. Any newer content overwrites local content. New content since last sync is then pushed to the storage target, overwriting any content on target if present.
  * `push`: Content is always pushed to the storage target, overwriting any existing content.
  * `pull`: Content is always pulled from the storage target, overwriting any local content which already exists.
* **defaultMode**: The default value from the choices listed above. Usually `push`.
* **schedule**: An [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601#Time_intervals) formatted time interval at which the sync function will be triggered or `false` to disable.
* **props**: An object of user editable properties. See [Module Properties](/dev/module-properties) for more info.
* **actions**: *(optional)* A list of manual actions the administrator can execute on this storage module.
  * **handler**: Function name that will be called
  * **label**: Pretty name of the function
  * **hint**: Description of what the action does.

## storage.js

This file contains methods that will be called when a new page is created, modified, deleted, etc.

```javascript
module.exports = {
  async activated () {
​
  },
  async deactivated () {
​
  },
  async init () {
  
  },
  async created (page) {
​
  },
  async updated (page) {
​
  },
  async deleted (page) {
​
  },
  async renamed (page) {
​
  },
  async sync () {
  
  }
}
```

All methods are required and must be implemented unless specified otherwise.

### activated

Upon activation of the storage module from the administration area. This is usually where storage prerequisites are checked _\(e.g. check settings, try to connect, create container, initialize repository, etc.\)._ 

```javascript
async activated () { }
```

Use **this.config** inside the method to access the configuration of the storage strategy. For example, if you defined properties `clientId` and `clientSecret` for the module props, `this.config` will be an object with properties `clientId` and `clientSecret` containing the values entered by the user in the administration area.

Any error thrown \(or returning a rejected promise\) will be reported to the user and the storage strategy will not be enabled.

### deactivated

Upon deactivation of the storage module from the administration area. This is where you disconnect from the storage provider if required. You should **never delete any content** upon deactivation, as the user may choose to re-enable this storage strategy later or simply want to keep the current content as backup.

```javascript
async deactivated () { }
```

**this.config** is an object containing the configuration of the storage strategy. See the [activated](#activated) event for more details.

Any error thrown \(or returning a rejected promise\) will be reported to the user and the storage strategy will not be disabled.

### init

Upon initialization of Wiki.js \(both startups or restarts\) and directly after the `activated` event. This is useful to establish a connection in some storage strategies.

```javascript
async init () { }
```

**this.config** is an object containing the configuration of the storage strategy. See the [activated](#activated) event for more details.

Any error thrown \(or returning a rejected promise\) will prevent the storage strategy from being used until Wiki.js is restarted or the error is acknowledged by the user in the administration area.

### created

Upon creation of a new page.

```javascript
async created (page) { }
```

Use **this** context inside the method to access following properties:

```javascript
{
    config: Object // Object containing the storage configuration
}
```

The first argument **page** has the following properties:

```javascript
    {
        id: Number, // Unique ID of the page
        localeCode: String, // 2 letter code (e.g. en).
        path: String, // Unique path of the page (e.g. some/page)
        title: String, // Title of the page
        description: String, // Short description of the page
        isPrivate: Boolean, // Is the page inside the user private namespace
        isPublished: Boolean, // Is the page published
        publishStartDate: String, // ISO-8601 Date (YYYY-MM-DDTHH:mm:ss.sssZ)
        publishEndDate: String, // ISO-8601 Date (YYYY-MM-DDTHH:mm:ss.sssZ)
        contentType: String, // The content original type (e.g. markdown, html, etc.)
        content: String, // The content
        createdAt: String, // ISO-8601 Date (YYYY-MM-DDTHH:mm:ss.sssZ)
        authorId: Number, // The Unique ID of the author
        authorName: String, // The full name of the author
        authorEmail: String // The email address of the author
    }
```

Any error thrown \(or returning a rejected promise\) will be logged but will not prevent the page from being created internally.

### updated

Upon modification of a page contents.

```javascript
async updated (page) { }
```

Use **this** context inside the method to access following properties:

```javascript
{
    config: Object // Object containing the storage configuration
}
```

The first argument **page** has the following properties:

```javascript
{
    id: Number, // Unique ID of the page
    localeCode: String, // 2 letter code (e.g. en).
    path: String, // Unique path of the page (e.g. some/page)
    title: String, // Title of the page
    description: String, // Short description of the page
    isPrivate: Boolean, // Is the page inside the user private namespace
    isPublished: Boolean, // Is the page published
    publishStartDate: String, // ISO-8601 Date (YYYY-MM-DDTHH:mm:ss.sssZ)
    publishEndDate: String, // ISO-8601 Date (YYYY-MM-DDTHH:mm:ss.sssZ)
    contentType: String, // The content original type (e.g. markdown, html, etc.)
    content: String, // The content
    createdAt: String, // ISO-8601 Date (YYYY-MM-DDTHH:mm:ss.sssZ)
    updatedAt: String, // ISO-8601 Date (YYYY-MM-DDTHH:mm:ss.sssZ)
    authorId: Number, // The Unique ID of the author (user updating the page)
    authorName: String, // The full name of the author (user updating the page)
    authorEmail: String, // The email address of the author (user updating the page)
    creatorId: Number, // The Unique ID of the user that first created the page
    creatorName: String, // The full name of the user that first created the page
    creatorEmail: String // The email address of the user that first created the page
}
```

Any error thrown \(or returning a rejected promise\) will be logged but will not prevent the page from being updated internally.

### deleted

Upon deletion of a page.

```javascript
async deleted (page) { }
```

Use **this** context inside the method to access following properties:

```javascript
{
    config: Object // Object containing the storage configuration
}
```

The first argument **page** has the following properties:

```javascript
{
    id: Number, // Unique ID of the page
    localeCode: String, // 2 letter code (e.g. en).
    path: String, // Unique path of the page (e.g. some/page)
    title: String, // Title of the page
    description: String, // Short description of the page
    isPrivate: Boolean, // Is the page inside the user private namespace
    createdAt: String, // ISO-8601 Date (YYYY-MM-DDTHH:mm:ss.sssZ)
    deletedAt: String, // ISO-8601 Date (YYYY-MM-DDTHH:mm:ss.sssZ)
    authorId: Number, // The Unique ID of the author (user deleting the page)
    authorName: String, // The full name of the author (user deleting the page)
    authorEmail: String, // The email address of the author (user deleting the page)
    creatorId: Number, // The Unique ID of the user that first created the page
    creatorName: String, // The full name of the user that first created the page
    creatorEmail: String // The email address of the user that first created the page
}
```

Any error thrown \(or returning a rejected promise\) will be logged but will not prevent the page from being deleted internally.

### renamed

Upon rename of a page or when a page is moved to another location.

```javascript
async renamed (page) { }
```

Use **this** context inside the method to access following properties:

```javascript
{
    config: Object // Object containing the storage configuration
}
```

The first argument **page** has the following properties:

```javascript
{
    id: Number, // Unique ID of the page
    localeCode: String, // 2 letter code (e.g. en).
    sourcePath: String, // Previous path of the page (e.g. some/oldpage)
    destinationPath: String, // New path of the page (e.g. some/newpage)
    title: String, // Title of the page
    description: String, // Short description of the page
    isPrivate: Boolean, // Is the page inside the user private namespace
    isPublished: Boolean, // Is the page published
    publishStartDate: String, // ISO-8601 Date (YYYY-MM-DDTHH:mm:ss.sssZ)
    publishEndDate: String, // ISO-8601 Date (YYYY-MM-DDTHH:mm:ss.sssZ)
    contentType: String, // The content original type (e.g. markdown, html, etc.)
    content: String, // The content
    createdAt: String, // ISO-8601 Date (YYYY-MM-DDTHH:mm:ss.sssZ)
    updatedAt: String, // ISO-8601 Date (YYYY-MM-DDTHH:mm:ss.sssZ)
    authorId: Number, // The Unique ID of the author (user renaming the page)
    authorName: String, // The full name of the author (user renaming the page)
    authorEmail: String, // The email address of the author (user renaming the page)
    creatorId: Number, // The Unique ID of the user that first created the page
    creatorName: String, // The full name of the user that first created the page
    creatorEmail: String // The email address of the user that first created the page
}
```

Any error thrown \(or returning a rejected promise\) will be logged but will not prevent the page from being renamed internally.

### sync

> *Should only be implemented if a schedule is defined in the module properties.*

Upon schedule trigger.

```javascript
async sync () { }
```

Use **this** context inside the method to access following properties:

```javascript
{
    config: Object, // Object containing the storage configuration
    mode: String // The selected sync mode (sync, push or pull)
}
```

Any error thrown \(or returning a rejected promise\) will be logged.