---
title: Internet Access
description: Learn about what content is downloaded from the Internet
published: true
date: 2019-11-10T17:56:23.669Z
tags: 
---

Wiki.js will regularly check for new content and updates.
This ensures your wiki is always up-to-date and that you can be notified of new versions of Wiki.js in the administration area.

# System Requests

- New **updates** are checked every 24h.
- New **language updates** are checked every 24h.

These requests are made to `graph.requarks.io`, a cloud service managed by the developers of Wiki.js. No tracking data or private information about your wiki is sent to the servers. Only the data necessary to process your request at hand is sent (such as your IP and the data requested) and is not stored afterwards.

An alternate method of downloading and [sideloading content](/install/sideload) (such as language files) is provided to allow for full offline installations.

# Module Requests

Some modules require internet access to function.

- Any **storage** modules you enable will communicate with the associated service provider at the schedule interval you specified in the administration area.
- Any **authentication**, **logging** and **search** modules you enable will communicate with the associated service provider on specific events (such as login, search queries and logging event).

> Note that some modules use libraries provided by service providers which may track and collect data. Make sure you trust the service provider before enabling a module.
{.is-warning}

# Telemetry

Telemetry provides useful insights to the developers to improve Wiki.js, as detailed in the [Telemetry](/telemetry) article.