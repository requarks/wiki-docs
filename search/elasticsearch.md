---
title: Elasticsearch
description: Search Engine Module
published: true
date: 2019-09-15T02:44:34.625Z
tags: 
---

Elasticsearch is a distributed, RESTful search and analytics engine capable of solving a growing number of use cases.

# Setup

1. In the Wiki.js administration area, click on **Search Engine** in the sidebar.
1. Select **Elasticsearch** as the search engine.
1. Select the **Elasticsearch Version** to use. This should match the version of Elasticsearch you are using.
1. Enter the **Host(s)** to connect to. This can be a single host or a list of comma-separated hosts. Make sure to include the port (e.g. `es.yourdomain.com:9200`). If you are using the Security extension of the Stack features pack (formally X-Pack), include the username and password as part of the URL.
1. Enter the desired **Index Name** (default: wiki). Do not create this index yourself as it will be created automatically.
1. <kbd>Advanced</kbd> Optionally enable the **Sniff on start** option to automatically attempt to discover the rest of the Elasticsearch cluster upon connecting. You can also specify the time interval to check for an updated list of nodes using the **Sniff interval** field. A value of `0` will disable this check.

Note that if you already have content in your wiki, you must click on **Rebuild Index** afterwards to import all your existing content into the search engine. Any change (new, edit, delete page) will be handled automatically from this point forward.

<img src="https://static.requarks.io/logo/elasticsearch.svg" alt="" class="align-abstopright" style="width: 150px;">