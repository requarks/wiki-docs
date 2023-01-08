---
title: Azure Search
description: Search Engine Module
published: true
date: 2019-09-15T02:43:58.623Z
tags: 
---

Azure Search is an AI-Powered cloud search service for web and mobile app development.

# Setup

1. Login to your [Azure portal](https://portal.azure.com)
1. Create a new **Azure Search** instance .
1. In the Wiki.js administration area, click on **Search Engine** in the sidebar.
1. Select **Azure Search** as the search engine.
1. Enter the **service name** of the Azure Search instance you just created. This is the name you entered when creating the new instance.
1. Enter either the primary or secondary admin key, found under **Keys** in the Azure portal.
1. Enter the desired index name (default: wiki).
1. Click the **Apply** button to save and initialize the search engine. An index will be created automatically.

Note that if you already have content in your wiki, you must click on **Rebuild Index** afterwards to import all your existing content into the search engine. Any change (new, edit, delete page) will be handled automatically from this point forward.

<img src="https://static.requarks.io/logo/azure.svg" alt="" class="align-abstopright" style="width: 200px;">