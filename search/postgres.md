---
title: DB - PostgreSQL
description: Search Engine Module
published: true
date: 2019-07-20T02:55:00.609Z
tags: 
---

This engine makes use of the advanced capabilities of PostgreSQL to provide a "good enough" search solution.

> :warning: You must be running Wiki.js using a PostgreSQL database in order to use this engine!
{.is-warning}

# Requirements

The **pg_trgm** extension must be enabled on the PostgreSQL for this engine to function correctly. It is enabled by default on most installations, but if that's not the case, you can enable it by running:

```sql
CREATE EXTENSION pg_trgm;
```

# Setup

1. In the Wiki.js administration area, click on **Search Engine** in the sidebar.
1. Select **DB - PostgreSQL** as the search engine.
1. Select the dictionnary language to use in the dropdown list.
1. Click the **Apply** button to save and initialize the search engine. An index will be created automatically.

Note that if you already have content in your wiki, you must click on **Rebuild Index** afterwards to import all your existing content into the search engine. Any change (new, edit, delete page) will be handled automatically from this point forward.