---
title: Troubleshooting
description: Common issues and solutions
published: true
date: 2019-09-15T02:49:40.335Z
tags: 
---

# Cannot upload files larger than X

**Cause:** You are most likely using a reverse proxy such as nginx or apache.

**Resolution**: Increase your reverse proxy configuration for file uploads.

# Cloudflare - JS / CSS / Emojis fail to load

**Cause:** CloudFlare performs some "optimizations" to some files during delivery. This breaks the integrity signatures of the files which are then blocked by the browser.

**Resolution**: In the Cloudflare dashboard for your site, create a new Page Rule. Enter the root path, in the following format: `wiki.yourdomain.com/*` and add the following settings:

- **Auto Minify**: Uncheck all
- **Mirage**: Off
- **Rocket Loader**: Off

Save and Deploy.

# Errors when using a subdirectory reverse-proxy

**Cause**: Wiki.js cannot be used / installed in a subfolder.

**Resolution**: Use a sub-domain instead (e.g. `wiki.yourcompany.com`).

# Links inside emails are incorrect

**Cause**: You did not set the `Site URL` in the **Administration Area**.

**Resolution**: In the **Administrator Area**, under **General**, set the **Site Url**.

# MySQL - Client does not support authentication protocol requested by server; consider upgrading MySQL client

**Cause**: The user used by Wiki.js to connect to the DB must use `mysql_native_password`. The newer `caching_sha2_password` method introduced in MySQL 8.0 is not yet supported in Node.js. Support will be added when the functionnality is made available in Node.js drivers.

**Resolution**: You can change an existing user to use a `mysql_native_password` using:

```sql
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
```

![](https://a.icons8.com/IMfhdRiW/YNcdYW/svg.svg){.align-abstopright}