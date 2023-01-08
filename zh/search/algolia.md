---
title: Algolia
description: Search Engine Module
published: true
date: 2019-09-15T02:43:22.304Z
tags: 
---

Algolia is a powerful search-as-a-service solution, made easy to use with API clients, UI libraries, and pre-built integrations.

# Setup

1. In the Wiki.js administration area, click on **Search Engine** in the sidebar.
1. Select **Algolia** as the search engine.
1. Enter your **Application ID**, found under the **API Keys** in your Algolia dashboard.
1. Enter your **Admin API Key**, found on the same page as before. You may also create a key specific to your wiki.
1. Enter the desired index name (default: wiki).
1. Click the **Apply** button to save and initialize the search engine. An index will be created automatically.

Note that if you already have content in your wiki, you must click on **Rebuild Index** afterwards to import all your existing content into the search engine. Any change (new, edit, delete page) will be handled automatically from this point forward.

![](https://static.requarks.io/logo/algolia.svg =x50){.align-abstopright}