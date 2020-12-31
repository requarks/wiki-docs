---
title: Themes
description: Customize the look & feel of your wiki
published: true
date: 2020-12-31T19:11:02.344Z
tags: 
editor: markdown
dateCreated: 2020-04-26T03:57:51.368Z
---

# Overview

Wiki.js comes bundled with a default theme, which supports both light and dark mode, and should be sufficient for most users.

# Download new themes

**It's not yet possible to change or download new themes.** This is planned for a future release.

# Create your own theme

> :warning: **Custom themes are not yet fully supported.** It's however possible to manually create one and compile it as part of the bundle.
>
> *The instructions below are for developers that are comfortable with Node.js / Vue.js development.*
{.is-danger}

## What can be customized

All aspects of a content page can be modified, **with the except of the header** (top black navigation bar). Because the header is dynamic and used consistently across all parts of the wiki (admin, editor, profile, etc.), it cannot be modified.

## Getting Started

You'll first need to [setup your dev environment](/dev) before going any further.

## Theme Structure

From the `client/themes` folder. Create a copy of the `default` folder and rename it to anything you like (e.g. `mytheme`). The folder name must be lowercase, no spaces or special characters.

A theme folder is composed of the following elements:

- **components**: Vue components (the view) for page, sidebar, footer, etc. elements. The entry point is `page.vue` and is mandatory.
- **js**: Javascript code specific to your theme. The entry point is `app.js` and is mandatory *(can be an empty file)*.
- **scss**: SCSS code specific to your theme. The entry point is `app.scss` and is mandatory *(can be an empty file)*.
- **theme.yml**: Your theme manifest (info about your theme).
- **thumbnail.png**: A thumbnail preview image of your theme.

## Development

Use the `yarn dev` command to start Wiki.js in development mode. Any changes you make to your theme will automatically rebuild the client assets.

### Activate your custom theme

In order for Wiki.js to use your theme, you must first set it as the active theme. It's not possible to do it via the Administration Area just yet. You'll need to modify the database directly:

- In the `settings` table, locate the `theming` row and edit the JSON value field.
- Change the `theme` property to the name of the folder you created earlier and commit the change.
- Restart your wiki for the change to be applied. (You can type `rs` + <kbd>ENTER</kbd> in your terminal to automatically reload the server)
- Your theme is now active.

### Modify components

The `components/page.vue` is the main view. You can include other components from here.

> The `props` object and the `created()` method **must stay intact**! This is where page data is persisted to the store and is used across the application. Altering them can break the whole page!
{.is-warning}

## Compile + Deploy

Once your theme is ready, you need to compile the project for deployment.

> Note that you will need to modify your production database to use your custom theme as well. Use the same instructions as above.
{.is-info}

### Using Docker

Run the docker build command below (changing the tag to your own docker repository name):

```bash
docker build -f dev/build/Dockerfile -t my-org/wiki:some-tag .
```

### Manually

Run the build command:
```bash
yarn build
```

This will generate a new folder named `assets` along with views under the `/server/views` folder. Copy + Paste both folders to your production server and restart your wiki.
