---
title: Troubleshooting
description: Common issues and solutions
published: true
date: 2022-12-11T02:59:52.328Z
tags: setup, guide
editor: markdown
dateCreated: 2019-04-08T05:56:27.927Z
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

# Error: Listening on port XX requires elevated privileges!

**Cause**: Some Linux installations prevent Node.js from binding to ports in the lower range *(e.g. < 1024)*. This occurs if you set a port such as 80 in config.yml.

**Solution A**: Allow the node process to safely access the port requested:

```bash
# Ubuntu / Debian

sudo apt-get install libcap2-bin
sudo setcap cap_net_bind_service=+ep `readlink -f \`which node\``
```

**Solution B**: Create a port redirection rule: *(In the example below, you must set the port to 3000 in config.yml)*

```bash
sudo iptables -t nat -A PREROUTING -i eth0 -p tcp --dport 80 -j REDIRECT --to-port 3000
```

**Solution C**: Use a web server in front of Wiki.js. For example, use nginx to listen to port 80 / 443 and proxy all requests to Wiki.js running on a higher port *(e.g. 3000)*.

# Error: Port XX is already in use!

**Cause**: Another program is already listening to this port.

**Resolution**: Use another port for Wiki.js or look for applications that could be using this port (web servers, http applications, etc.) and stop them.

# Error: Unknown authentication strategy "jwt"

**Cause**: This error is shown when attempting to load the site before the server is done initializing.

**Resolution**: Simply reload the page again. If the error still occurs after a while, check your server logs for an error preventing Wiki.js from fully initializing.

# How to execute javascript code on page load

You may have noticed that running javascript code on the standard page load or dom ready event don't work because the page content isn't rendered yet.

You need to register a callback via `window.boot.register(evt, clb)` instead, where the triggering event is `page-ready`, e.g.:

```js
window.boot.register('page-ready', () => {
	// code to execute
})
```

Your code will now execute once the page is loaded and the Vue instance is ready.

# How to hide the footer Wiki.js mention

**Seriously?** This software is provided to you completely free. Volunteers have put thousands of hours of their time into this project. We believe a small mention in the footer is a very small thing to ask in return...

# How to manually disable HTTPS / SSL Redirection

If you are unable to load the site because of a SSL certificate error, you can manually disable SSL Redirection.

In the database, under the `settings` table, you must set the `sslRedir` property to false for the `server` key.
Restart Wiki.js to load the new setting.

### For docker users

When running PostgreSQL inside a docker container (e.g. DigitalOcean / AWS official image), you can run the following commands:

```bash
docker exec db psql -U wiki -d wiki -c "DELETE FROM settings WHERE key = 'server';"
docker restart wiki
```

# How to manually reset the admin password?

The only way to change a password, without access to the web UI, is via the database. Use a tool like **pgAdmin** *(postgres)*, **DBeaver** *(mysql, mariadb)*, **SQL Management Studio** *(mssql)* or **DB Browser for SQLite**.

Connect to your DB, browse to the `users` table and locate your user.

Edit the password column and insert a new **bcrypt**-formatted value. You can use a tool like https://bcrypt-generator.com/ to generate one. The number of rounds must be **12**.

> **It is NOT possible to read the current password value.** Passwords are stored using a one-way bcrypt hashing process, which is not reversible. You can only overwrite it with a new value.
{.is-warning}

### For docker users

When running PostgreSQL inside a docker container (e.g. DigitalOcean / AWS official image), follow these steps:

1. Use a tool like https://bcrypt-generator.com/ to generate a bcrypt hash of the password you want. The number of rounds must be **12**.
2. Connect to your machine / droplet via SSH.
3. Run the following command, replacing `HASH-PASSWORD` with the hash generated in step 1 and `YOUR-EMAIL` with the email address of the account you want to reset:

```bash
docker exec db psql -U wiki -d wiki -c "UPDATE users SET password = 'HASH-PASSWORD' WHERE email = 'YOUR-EMAIL';"
```

# Links inside emails are incorrect

**Cause**: You did not set the `Site URL` in the **Administration Area**.

**Resolution**: In the **Administrator Area**, under **General**, set the **Site Url**.

# MySQL - Client does not support authentication protocol requested by server; consider upgrading MySQL client

**Cause**: The user used by Wiki.js to connect to the DB must use `mysql_native_password`. The newer `caching_sha2_password` method introduced in MySQL 8.0 is not yet supported in Node.js. Support will be added when the functionnality is made available in Node.js drivers.

**Resolution**: You can change an existing user to use a `mysql_native_password` using:

```sql
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
```

# Some HTML tags are rendered as plain text

Starting in version **2.1**, a new HTML sanitization step is added by default to the rendering pipeline. This feature prevents potentially unsafe HTML tags / properties from being present in the final render. Any HTML tag or property that isn't whitelisted will be rendered as plain text.

If you are the sole editor / trust your editors, you can disable this feature in the **Administration Area**, under **Rendering** > **HTML** > **Security** > **Sanitize HTML**.

# Unable to upgrade from the Administration Area

If clicking the <kbd>Perform Upgrade</kbd> button doesn't actually upgrade the wiki instance, you need to upgrade the wiki-update-companion container to the latest version. A bug was present in an earlier version that failed to properly fetch the latest image.

Assuming you're running the [DigitalOcean Wiki.js droplet](/install/digitalocean) or you followed the [Ubuntu Install Guide](/install/ubuntu), connect to your server via SSH and run the following commands:

```
docker stop wiki-update-companion
docker rm wiki-update-companion
docker pull ghcr.io/requarks/wiki-update-companion:latest
docker create --name=wiki-update-companion -v /var/run/docker.sock:/var/run/docker.sock:ro --restart=unless-stopped -h wiki-update-companion --network=wikinet ghcr.io/requarks/wiki-update-companion:latest
docker start wiki-update-companion
```

The <kbd>Perform Upgrade</kbd> button should now work correctly.

![](https://a.icons8.com/IMfhdRiW/YNcdYW/svg.svg){.align-abstopright}