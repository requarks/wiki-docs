---
title: Modules
description: Introduction to Modules for developers
published: true
date: 2022-06-12T21:10:33.633Z
tags: dev
editor: markdown
dateCreated: 2019-02-15T04:25:49.728Z
---

Wiki.js 2.0 introduces a fully modular approach to critical components such as authentication and storage. This allows developers to easily integrate the app with their existing infrastructure.

All modules are located under `server/modules`.

In-depth guides for available for each module type:

* [Authentication](/dev/authentication)
* [Comments](/dev/comments)
* [Rendering](/dev/rendering)
* [Search Engine](/dev/search)
* [Storage](/dev/storage)
{.links-list}

Modules share the same basic structure. They consist of a definition file (`definition.yml`), which contains info and configuration of your module, and a code file where the actual logic resides. Modules are completely self-contained and do not run within the same context as the core Wiki.js app unless explicitly specified in the documentation. This also means that any dependencies not included by default with Wiki.js must reside in the module directory.

## Module Dependencies

Some modules may require npm dependencies not present in the main Wiki.js package.json. Verify first that the dependency you need isn't already in the main project. **DO NOT add dependencies to the main package.json**. This is reserved for the core Wiki.js app only and doing so can introduce breaking changes. 

If the package you need isn't already present, you must instead install extra dependencies within the same folder as your module definition file. You must first create a local package.json from your module directory:

```bash
npm init
```

Accept all the defaults. You can now add local dependencies:

```bash
npm install your-dependency
```

This will create a `node_modules` folder and install the dependency locally. You can then `require()` the module in your code.

> **Do not use natively compiled dependencies** \(packages that use node-gyp or download os specific executables\). These require build tools \(such as python, c++ compilers, etc.\) which will not be present on customers machines and will usually fail to install on low memory systems.
{.is-danger}

![](https://a.icons8.com/Ufcf0eoh/d5D6Em/svg.svg){.align-abstopright}