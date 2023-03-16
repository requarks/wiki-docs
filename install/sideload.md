---
title: Sideloading
description: Enable your wiki to run without internet access
published: true
date: 2020-07-04T21:15:31.336Z
tags: 
editor: markdown
---

# Basics

If your wiki is installed in an environment which is isolated from the internet, you can sideload data that would normally be downloaded from the internet.

This is achieved by manually downloading a set of files and placing them in a specific directory in your wiki installation. These files will be imported during initialization.

## Getting Started

**Create a new folder** at path `data/sideload` inside your Wiki.js installation folder.
*For example, if your wiki is installed at path `/home/wiki`, you'd need to create a folder at path `/home/wiki/data/sideload`*

# Locales

In order to install locale packages, you need the **master locale file** + at least one **locale package file**.

> The files can be downloaded from https://github.com/Requarks/wiki-localization. These files are made up to date every night.
{.is-info}

## 1 - Master File

The master file `locales.json` contains information about all available languages and is **REQUIRED** to install any locale.

Place this file inside the `sideload` folder created previously.

## 2 - Locale Packages

The locale package file `xx.json` or `xx-zz.json` contains all the translations for the language(s) of your choice. You can sideload any number of locales at the same time.

> The English package `en.json` is **REQUIRED**, as this is the default language during installation. You can change the language afterwards.
{.is-warning}

Place the file(s) inside the `sideload` folder created previously alongside the master file. You should now have `locales.json`, `en.json` and any additional languages in your folder.

## 3 - Sideload

Run Wiki.js (or restart the process if already running) to automatically sideload the files localed in the `data/sideload` folder.

> Because of a bug in versions prior to 2.5, the locale files are loaded in incorrect order, causing the clients to be unable to fetch the translations.
> 
> As a workaround, once Wiki.js is fully started, restart the server again. The locale data (which is now in the database) will be loaded correctly.
{.is-danger}

# Themes

*Coming soon*