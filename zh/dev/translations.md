---
title: Translations
description: Contribute a new language or test new keys
published: true
date: 2020-05-17T06:05:42.143Z
tags: dev, localization
---

# Contribute a new / existing language

We are always looking for translation contributors to make Wiki.js accessible in as many language as possible!

You can join our Lokalise project below to gain access to the translation tools. No coding required! Feel free to contact us on [Slack](https://wiki.requarks.io/slack) if you have any questions!

> **Only select the language(s) you're going to actively contribute to!** Users that select too many or all languages at once will be removed.
{.is-warning}

[![btn-join-the-project.png](/assets/buttons/btn-join-the-project.png)](https://lokalise.com/public/2994254859f751ea605a00.03473540/)

If you can't find your language in the list, contact us on [Slack](https://wiki.requarks.io/slack) and we'll add it!

# View latest changes on your wiki

There're various layers of cache before changes made to translations become visible in your wiki:

- The Requarks GraphQL server caches translations **every 5 minutes**.
- Your wiki installation fetches changes from the Requarks GraphQL server **every 24 hours**.
- If you're using offline sideloading, [locale files](https://github.com/Requarks/wiki-localization) are updated every day at **12:00 AM Eastern Standard Time (EST)**.

It's possible to force changes to be fetched immediately by restarting your Wiki.js instance. A job to fetch updated translations will start immediately after initialization. *Note that you must still wait the 5 minutes delay from the Requarks GraphQL server before seeing any updates.*

> **Browser Cache**
>
> Translations are kept in the browser cache for 24h. Even though your Wiki.js instance could have the latest changes, you will not see them until the browser cache expires. You can flush this cache from the **Administration Area** > **Utilities** > **Flush Cache** > **Flush Client-Side Locale Cache**.
{.is-info}

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