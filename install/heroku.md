---
title: Heroku
description: Getting started with a Wiki.js installation on Heroku
published: true
date: 2021-03-01T06:39:40.092Z
tags: setup
editor: markdown
dateCreated: 2019-05-04T04:37:42.209Z
---

Heroku is a popular platform to quickly run any type of web application.

A preconfigured deploy template is provided for convenience:

[![Deploy](https://www.herokucdn.com/deploy/button.svg)](https://heroku.com/deploy?template=https://github.com/requarks/wiki-heroku/tree/2.x)

# Important Notes

- The deployment template will use the default PostgreSQL plan, which is the Hobby Dev (free) plan. You can upgrade to a larger plan afterwards as detailed in the [Heroku docs](https://devcenter.heroku.com/articles/updating-heroku-postgres-databases). Another option is to clone the [wiki-heroku](https://github.com/Requarks/wiki-heroku/tree/2.x) repository and edit the manifest to use the specific plan you need.
- While the initial deployment is extremely quick and easy, **upgrading to a new version is not**. You'll need to push a new commit to your app git repo in order to trigger a new build. Unless you are comfortable with the Heroku workflow for deployments, you may want to look into alternative hosting solutions instead.
- The free dyno plan (default) will "sleep" after 30 mins of inactivity. The first page load after such event will take several seconds to complete, as it must spin a new instance. Upgrade to a paid dyno plan to remove this limitation.
- The database endpoint must be provided as `DATABASE_URL` environment variable to the app (default).

# DB Connection Bug

A Heroku-specific bug preventing Wiki.js from connecting to the database by default. The root cause has not yet been identified.

A workaround, which involves downgrading the database to PostgreSQL 10, is provided in this ticket:

https://github.com/Requarks/wiki/issues/2949#issuecomment-773412440

![](https://a.icons8.com/TgwPdfer/uNiaiQ/svg.svg){.align-abstopright}
