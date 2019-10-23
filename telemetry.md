---
title: Telemetry
description: Help us improve Wiki.js!
published: true
date: 2019-10-23T01:43:18.259Z
tags: 
---

# What is telemetry?
Telemetry allows the developers of Wiki.js to improve the software by collecting basic **anonymized** data about its usage and the host info.

This is entirely **OPTIONAL** and **absolutely NO private data** (such as content or personal data) is collected.

For maximum privacy, a random client ID is generated during setup. This ID is used to group requests together (instead of IP addresses) while keeping complete anonymity.

# What is collected?
When telemetry is enabled, only the following data is transmitted:

- Version of Wiki.js installed
- Basic OS information:
	- Platform type *(Linux, macOS or Windows)*
  - Total CPU Cores
  - Type of DB *(PostgreSQL, MySQL, MariaDB, SQLite or SQL Server)*
- Crash debug data *(stack trace of the error)*
- Setup analytics *(installation checkpoint reached)*

Note that crash debug data is stored for a maximum of 30 days while analytics are stored for a maximum of 16 months, after which it is permanently deleted.

# What is it used for?

Telemetry is used by developers to improve Wiki.js, mostly for the following reasons:

- Identify critical bugs more easily and fix them in a timely manner.
- Understand the upgrade rate of current installations.
- Optimize performance and testing scenarios based on most popular environments.

Only authorized developers have access to the data. It is not shared to any 3rd party nor is it used for any other application than improving Wiki.js.

# How to enable / disable telemetry

Telemetry can be turned on / off during the installation wizard and anytime afterwards in the administration area under **Utilities** > **Telemetry**.

# How to reset the client ID

A random client ID is generated at the time of installation. This client ID is used to group requests together while providing complete anonymity. In case you want to continue sending telemetry but under a new random identifier, you can simply reset the client ID in the administration area under **Utilities** > **Telemetry**. A new random client ID will be generated and used for future transmissions.

# Questions / Feedback

Feel free to contact us on [Slack](https://wiki.requarks.io/slack) should you have any question or feedback on telemetry.

![](https://a.icons8.com/gojSbjmc/1rnPd3/svg.svg){.align-abstopright}