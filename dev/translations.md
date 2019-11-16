---
title: Translations
description: Contribute a new language or test new keys
published: true
date: 2019-11-16T21:23:21.384Z
tags: dev, localization
---

# Contribute a new / existing language

We are always looking for translation contributors to make Wiki.js accessible in as many language as possible!

You can [join the project](https://lokalise.com/public/2994254859f751ea605a00.03473540/) to gain access to the translation tools. No coding required! Feel free to contact us on [Slack](https://wiki.requarks.io/slack) if you have any questions!

# View latest changes on your wiki

There're various layers of cache before changes made to translations become visible in your wiki:

- The Requarks GraphQL server caches translations **every 5 minutes**.
- Your wiki installation fetches changes from the Requarks GraphQL server **every 24 hours**.
- If you're using offline sideloading, [locale files](https://github.com/Requarks/wiki-localization) are updated every day at **12:00 AM Eastern Standard Time (EST)**.

It's possible to force changes to be fetched immediately by restarting your Wiki.js instance. A job to fetch updated translations will start immediately after initialization. *Note that you must still wait the 5 minutes delay from the Requarks GraphQL server before seeing any updates.*

# How contributions are selected

Since multiple users can contribute to the same language, the following process is used:

- The edit with the most votes will be used;
- Otherwise, the most recent edit will be used;


# Development Mode

If you need to add new keys and test them live in your dev environment, simply create a {LANG}.yml file in the `server/locales` folder containing the values you want to test. e.g.:

### en.yml
```yml
admin:
  api.title: 'API Access'
  auth.title: 'Authentication'
```

The official localization keys will still be loaded first, but your local files will overwrite any existing keys (and add new ones).

Note that you must restart Wiki.js to load any changes made to the files, which happens automatically on save when in dev mode.