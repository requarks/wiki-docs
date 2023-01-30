---
title: Transfer Wiki.js between servers
description: How to migrate your installation to a new server
published: true
date: 2023-01-29T21:57:54.346Z
tags: 
editor: markdown
dateCreated: 2020-09-13T03:44:51.774Z
---

# Getting Started

This guide assumes you're currently using a **PostgreSQL** database installation of Wiki.js 2.x running on Docker on Linux, as detailed in the [Ubuntu installation guide](/install/ubuntu). This is the default installation method for 1-click images for DigitalOcean and AWS Marketplace.

> Note that it is **NOT** possible to "convert" an installation from a different database engine *(e.g. MySQL, MSSQL or SQLite)*. You should instead export content manually to disk and re-import it into a new installation.
{.is-danger}

# 1. Setup New Server

***Context:** New server*{.caption}

Let's start by setting up the destination server. Follow the [Ubuntu installation guide](/install/ubuntu) up until the "**Access the setup wizard**" step *(don't do this step, stop right after starting the Docker containers)*.

You should now have a fully setup server with a PostgreSQL database, a Wiki.js installation and the Wiki.js auto-updater all running in Docker containers.

# 2. Backup Database

***Context:** Old server*{.caption}

On your old server where your previous installation is located, make a full database dump:
```bash
docker exec db pg_dump wiki -U wiki -F c > wikibackup.dump
```
> In the above command, the PostgreSQL docker container is named `db` and we're using the database name `wiki` and user `wiki`. This is the default if you followed the tutorial mentionned in the Getting Started section above.
{.is-info}

This will create a new file `wikibackup.dump` in the current directory.

# 3. Transfer Backup

***Context:** Old server*{.caption}

We'll now transfer the backup file onto the new server. There're several methods to copy files between servers but we'll use rsync for this example. Replace `YOUR-NEW-SERVER-IP` in the command below with the IP address of your new server.

```bash
rsync -P wikibackup.dump root@YOUR-NEW-SERVER-IP:~/wikibackup.dump
```

> This assumes that you have previously configured your new server to accept SSH connections from your old server. To do so, you need to add the public key of the old server into the authorized_keys of the new server. You can learn how [in this tutorial](https://www.digitalocean.com/community/tutorials/how-to-set-up-ssh-keys-on-ubuntu-22-04).
{.is-info}

# 4. Restore Database

***Context:** New server*{.caption}

We're now ready to restore the database dump into the new database.

On the new server, stop the `wiki` docker container:

```bash
docker stop wiki
```

Restore the `wikibackup.dump` file into a new database, first dropping the existing empty DB:
```bash
docker exec -it db dropdb -U wiki wiki
docker exec -it db createdb -U wiki wiki
cat ~/wikibackup.dump | docker exec -i db pg_restore -U wiki -d wiki
```

We can now restart the `wiki` container:
```
docker start wiki
```

That's it!