---
title: Translations
description: Contribute a new language or test new keys
published: true
date: 2019-09-15T02:46:26.686Z
tags: 
---

# Contribute a new language

We are always looking for translation contributors to make Wiki.js accessible in as many language as possible!

Contact us on [Slack](https://wiki.requarks.io/slack) to request access to the translation tools. No coding required!

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