---
title: 2.0 Beta Release Notes
description: List of new features, bug fixes and improvements
published: true
date: 2020-01-26T20:43:49.043Z
tags: 
---

This is an archive of the release notes for the 2.0 Beta releases. For the current builds, read the [latest release notes](/releases) instead.

# 2.0.0-beta.303

> Released on **September 14th, 2019**
{.is-info}

> **Notice:** Avoid upgrading if you're using MS SQL Server as the database engine. A bug can render the wiki innaccessible. We are investigating the issue.
{.is-danger}

## Tags

Tags can now be added to any page to enable quick and simple categorization. These tags are displayed below the table of contents on every page.

A new **Browse Tags** page can be accessed by a button next to the top search bar. A list of matching pages to your tags selection will be shown and these results can be filtered / sorted.

## Rich-Text Visual Editor

In addition to the existing Markdown editor, you can now choose a WYSIWYG editor when creating new pages! Perfect for non-technical users or if you need to create complex tables.

## Link States

Links are now rendered differently based on whether the destination is an external site or an internal page. Links to non-existant pages are shown in red.

## Automatic Database Connection Retries on Start

In scenarios like Docker Compose where the database might not be ready yet when the first connection from Wiki.js is made would previously crash and end the process. In this new build, Wiki.js will now attempt to reconnect up to **10 times**, with a **3 seconds delay** between each attempts, leaving plenty of time for the database to finish initializing.

## AWS S3 + DigitalOcean Spaces Storage Modules

Content can now be backup to AWS S3 and DigitalOcean Spaces with these new modules! Thanks to [@andrewsim](https://github.com/andrewsim).

## Keycloak Authentication Module

Keycloak is now supported as an authentication strategy. Thanks to [@D4uS1](https://github.com/D4uS1).

## Bug fixes / Minor Improvements

- **Fixed:** Search results are now filtered according to the user access rights
- **Fixed:** Markdown Editor scroll sync
- **Fixed:** Insert Media Modal is now displayed correctly over the editor ([#992](https://github.com/Requarks/wiki/issues/992))
- **Fixed:** Page Not Found buttons are now displayed properly ([#990](https://github.com/Requarks/wiki/issues/990))
- **Fixed:** Vuetify not being transpiled for MS Edge ([#994](https://github.com/Requarks/wiki/issues/994))
- **Fixed:** Missing MDI icons on the registration dialog ([#996](https://github.com/Requarks/wiki/issues/996))
- **Fixed:** Local Disk Storage - non-default language entries would overwrite default language entries ([#1000](https://github.com/Requarks/wiki/issues/1000))
- **Fixed:** Incorrect default language selected in page-selector for new pages ([#1005](https://github.com/Requarks/wiki/issues/1005))
- **Fixed:** Links to anchors within the page now scrolls to target correctly ([#1006](https://github.com/Requarks/wiki/issues/1006))
- **Fixed:** Create an account link is now hidden when selecting a non-local strategy that is using the form.
- **Improvements:** Most recent pages are now listed in the admin dashboard.

## Links

- [Installation](/install)
- [Upgrade from previous Beta (Build 275)](/install/upgrade)

Consider supporting this project by [becoming a Patron](https://www.patreon.com/requarks) or donating to our [Open Collective](https://opencollective.com/wikijs).

# 2.0.0-beta.275

> Released on **August 26th, 2019**
{.is-info}

## Bug fixes / Minor Improvements

- **Fixed:** Login dialog is now displayed properly when using dark mode.
- **Fixed:** Unauthorized page buttons are now displayed correctly.
- **Fixed:** Saving / Creating a page with empty content now results in an error.
- **Fixed:** Incomplete ratings panel is now hidden.
- **Improvements:** Unauthorized access on the homepage now automatically redirects to the login page.
- **Improvements:** The help text on the Admin Navigation page has been clarified for Font Awesome 5 style classes.

## Links

- [Installation](/install)
- [Upgrade from previous Beta (Build 268)](/install/upgrade)

Consider supporting this project by [becoming a Patron](https://www.patreon.com/requarks) or donating to our [Open Collective](https://opencollective.com/wikijs).

# 2.0.0-beta.268

> Released on **August 25th, 2019**
{.is-info}

## Bug fixes

- **Fixed:** Welcome page after new install would crash ([#981](https://github.com/Requarks/wiki/issues/981))
- **Fixed:** Text above an anchor could not be selected within 75px.

## Links

- [Installation](/install)
- [Upgrade from previous Beta (Build 267)](/install/upgrade)

Consider supporting this project by [becoming a Patron](https://www.patreon.com/requarks) or donating to our [Open Collective](https://opencollective.com/wikijs).

# 2.0.0-beta.267

> Released on **August 25th, 2019**
{.is-info}

## Create / Pre-Authorize New Users

You can now manually create new local users or pre-authorize users from other authentication strategies!

## Material Design 2

The entire UI framework has been updated to the latest Material Design 2 version.

## Reworked Content Page Display

The content display has been reworked to allow for more content to be displayed at once. The table of contents has been moved to the left for easier navigation. The edit button is now prominently displayed at the bottom right corner of the page.

## Manage Security Policies

You can now turn on / off specific security policies from the Administration Area:

- Block iFrame Embedding
- Same Origin Referrer
- Enforce HSTS

## Bug fixes / Minor Improvements

- **Fixed:** GitLab BaseURL handling for self-hosted instances (Take 2) ([#934](https://github.com/Requarks/wiki/issues/934))
- **Fixed:** Anchor scrolling no longer goes past the header ([#953](https://github.com/Requarks/wiki/issues/953))
- **Improvements:** Arabic UI has been improved + dedicated arabic fonts.
- **Improvements:** Content is now displayed properly when in print mode.
- **Improvements:** Discord authentication prompt is now skipped ([#949](https://github.com/Requarks/wiki/issues/949)).

## Breaking Changes

Material Icons were deprecated in favor of the Material Design Icons. This means your icons will no longer work in the sidebar navigation.

Going forward, you must refer to https://materialdesignicons.com/ for icon choices and use the `mdi-` prefix. For example, if you wish to use the icon `baguette`, you would input `mdi-baguette`.

All icons that were present in the Material Icons library are available in the Material Design Icons library, albeit under slightly different names.

## Links

- [Installation](/install)
- [Upgrade from previous Beta (Build 241)](/install/upgrade)

Consider supporting this project by [becoming a Patron](https://www.patreon.com/requarks) or donating to our [Open Collective](https://opencollective.com/wikijs).

# 2.0.0-beta.241

> Released on **July 21st, 2019**
{.is-info}

## Azure AD Authentication Module

The Azure AD authentication module is now available! Check out the [docs](/auth/azure) on how to set it up.

## Bug fixes / Minor Improvements

- **Fixed:** FontAwesome 5 now loads the latest version.
- **Fixed:** Regional locales can now be referenced properly. **New installations only, no migration from existing betas* ([#926](https://github.com/Requarks/wiki/issues/926))
- **Fixed:** Dark grey background is no longer displayed before Vue is initialized. ([#817](https://github.com/Requarks/wiki/issues/817))
- **Improvements:** Ability to paste the contents of the private key for Git SSH connection.
- **Improvements:** Support for `<details>` and `<summary>` tags.
- **Improvements:** Warn before leaving editor with unsaved edits via back function.

## Links

- [Installation](/install)
- [Upgrade from previous Beta (Build 230)](/install/upgrade)

Consider supporting this project by [becoming a Patron](https://www.patreon.com/requarks) or donating to our [Open Collective](https://opencollective.com/wikijs).

# 2.0.0-beta.230

> Released on **July 14th, 2019**
{.is-info}

## Analytics

This build brings 4 new analytics modules:

- Matomo
- New Relic Browser
- StatCounter
- Yandex Metrica

## Icon Sets

It's now possible to use another set of icons for the sidebar navigation. It can be set from the **Theme** section.

- Material Design Icons
- Font Awesome 5
- Font Awesome 4

## Utilities

You can now perform various maintenance and troubleshooting tasks from the **Utilities** section:

### Authentication

- Generate New Authentication Public / Private Key Certificates
- Reset Guest User

### Cache

- Flush Pages & Assets Cache
- Flush Temporary Uploads
- Flush Client-Side Locale Cache

### Content

- Migrate all pages from source locale to target locale

### Telemetry

- Enable / Disable Telemetry
- Reset the Telemetry Client ID

## Simplified Setup

The setup experience has been improved and simplified to a single step.

## Legacy Display Mode

Pages will now display in a limited basic mode when using Internet Explorer.

## Bug fixes / Minor Improvements

- **Fixed:** Prevent pages from being created twice from the client
- **Fixed:** Handle pages with no rendered content
- **Fixed:** GitLab BaseURL handling for self-hosted instances ([#907](https://github.com/Requarks/wiki/issues/907))
- **Fixed:** Locales now correctly show as up-to-date when manually triggering the fetch.
- **Fixed:** Locale strings are now properly cached client-side. ([#912](https://github.com/Requarks/wiki/issues/912))
- **Fixed:** Editing actions are now hidden for guests.
- **Fixed:** Welcome page is now shown in correct locale whe not using base locale.
- **Fixed:** CSS Overrides are now included in the editor preview page. ([#915](https://github.com/Requarks/wiki/issues/915))
- **Improvements:** Admin Locales list now shows completion next to each language.
- **Improvements:** GitHub Enterprise is now supported as authentication strategy. ([#918](https://github.com/Requarks/wiki/issues/918))
- **Improvements:** Current path is now retained when inserting assets. ([#919](https://github.com/Requarks/wiki/issues/919))

## Links

- [Installation](/install)
- [Upgrade from previous Beta (Build 208)](/install/upgrade)

Consider supporting this project by [becoming a Patron](https://www.patreon.com/requarks) or donating to our [Open Collective](https://opencollective.com/wikijs).

# 2.0.0-beta.208

> Released on **June 24th, 2019**
{.is-info}

## Analytics

You can now enable one or more analytics module to monitor and track user sessions on your wiki. The following modules are supported:

- Azure Application Insights
- Countly
- Elasticsearch APM RUM
- Fathom Analytics
- FullStory
- Google Analytics
- Google Tag Manager
- Hotjar

## GitLab Authentication

A new authentication module is available: GitLab! It supports both cloud and self-managed instances.

## Bug fixes / Minor Improvements

- **Fixed:** Elasticsearch module has been upgraded with support for 6.x and 7.x ([#865](https://github.com/Requarks/wiki/issues/865))
- **Fixed:** Git and Local Disk storage modules would incorrectly push content of different languages over the same file when using namespacing.
- **Fixed:** Closing the editor on a non-default locale would incorrectly redirect to the site default locale version.

## Links

- [Installation](/install)
- [Upgrade from previous Beta (Build 203)](/install/upgrade)

Consider supporting this project by [becoming a Patron](https://www.patreon.com/requarks) or donating to our [Open Collective](https://opencollective.com/wikijs).

# 2.0.0-beta.203

> Released on **June 22nd, 2019**
{.is-info}

## Improved Localization

- Most UI elements have been localized and will now display properly in your language. The remaining elements will be localized soon!
- The Portuguese (Brazil) locale is now supported and future regional locales will now display correctly in the list of available locales.
- Right-to-left is now enabled across the app on supported languages. There're however still some display issues to iron out.

## Locale Namespacing

You can now create language variations of the same page and quickly switch between them from the top nav bar.

## Send Test Email feature

You can now send a test email from the Administration Area to check whether your SMTP configuration is correct.

## Sideloading for Offline Installations

It's now possible to use Wiki.js in a fully offline environment. Set the option `offline: false` in your `config.yml` to enable this mode.

You can now manually [sideload language files](/install/sideload).

## Bug fixes / Minor Improvements

- **Fixed:** Windows compatibility for SQLite installations ([#870](https://github.com/Requarks/wiki/issues/870))
- **Fixed:** Self-registration for the local strategy not assigning the default group
- **Fixed:** Headers 4 to 6 are now displayed properly.
- **Fixed:** Dev locale overriding is now working correctly. ([#880](https://github.com/Requarks/wiki/pull/880))
- **Fixed:** Error messages are now shown properly during setup ([#821](https://github.com/Requarks/wiki/pull/821))
- **Fixed:** All active locales are now updated automatically when selecting locale namespacing.
- **Fixed:** Media Modal in Editor would incorrectly show in mobile layout on some screen resolutions.
- **Fixed:** Absolute Top Right image alignment is now positioned and sized correctly.
- **Improvements:** Dark Theme UI for page content

## Links

- [Installation](/install)
- [Upgrade from previous Beta (Build 180)](/install/upgrade)

Consider supporting this project by [becoming a Patron](https://www.patreon.com/requarks) or donating to our [Open Collective](https://opencollective.com/wikijs).

# 2.0.0-beta.180

> Released on **June 5th, 2019**
{.is-info}

## Bug fixes / Minor Improvements

- **Fixed:** Disable DB SSL connection unless explicitely enabled
- **Fixed:** User search incorrectly caching results
- **Improvements:** Spaces are now replaced in upload filenames
- **Improvements:** LDAP Debug flag now available in Developer Tools > Flags
- **Improvements:** Admin mail + system pages translations

## Links

- [Installation](/install)
- [Upgrade from previous Beta (Build 174)](/install/upgrade)

Consider supporting this project by [becoming a Patron](https://www.patreon.com/requarks) or donating to our [Open Collective](https://opencollective.com/wikijs).

# 2.0.0-beta.174

> Released on **June 2nd, 2019**
{.is-info}

## Heroku Support

Heroku is now supported! Visit the [Heroku installation page](/install/heroku) for details.

## SSL Database Connection Support

A new option is now available to connect to a database server over SSL. You can use either:

- Set the `db.ssl` flag in your `config.yml` (refer to the [config.sample.yml](https://github.com/Requarks/wiki/blob/2.0.0-beta.174/config.sample.yml#L31)).
- Use the `DB_SSL` environment variable (set to any thruthy value).
- Use the `DATABASE_URL` environment variable with the full database connection string.

## Bug fixes / Minor Improvements

- **Fixed:** Red blockquote toolbar menu using incorrect class ([#854](https://github.com/Requarks/wiki/issues/854))
- **Fixed:** Page hangs when attempting to create a 2 letters page
- **Fixed:** HTTP git url composed incorrectly ([#861](https://github.com/Requarks/wiki/issues/861))
- **Improvements:** General UI enhancements
- **Improvements:** Updated package dependencies

## Links

- [Installation](/install)
- [Upgrade from previous Beta (Build 147/148)](/install/upgrade)

Consider supporting this project by [becoming a Patron](https://www.patreon.com/requarks) or donating to our [Open Collective](https://opencollective.com/wikijs).

# 2.0.0-beta.148/147

> Initially released on **May 26th, 2019** as `2.0.0-beta.147`. An hotfix was released on **May 27th, 2019** for MySQL/MariaDB installations as `2.0.0-beta.148`.
{.is-info}

## Assets

Assets such as images and files can now be uploaded and inserted into your pages!

![Assets](/assets/release-notes/beta147-assets.png =1000x510){.decor-shadow .radius-4}

### Upload Files

Upload multiple files *(up to 10 at a time)* by clicking the **Browse...** button or using drag-n-drop on the grey area.

Press **Upload** when you're ready to send the files to the server. They will appear in the assets listing automatically.

### Folders

Categorize your files inside folders. It's now possible to create nested folders as well.

Folder operations *(such as rename / delete a folder)* will come in a future build.

### Context Menu

This beta build ships with 2 functions:

- **Rename**
- **Delete**

Other functions will ship in a future build.

### Image Alignment

Use the dropdown menu on the right to change the alignment of your image.

## Markdown Toolbar

The toolbar in the Markdown editor is now fully functional.

![ui-markdown-toolbar.png](/assets/ui/ui-markdown-toolbar.png =400x){.decor-shadow .radius-4}

## Decoration Classes

### Links List

Use the `links-list` class to style your lists of links:

```
- [Link 1](/link1)
- [Link 2](/link2)
{.links-list}
```
will generate:

- [Link 1](/link1)
- [Link 2](/link2)
{.links-list}

### Grid List

Use the `grid-list` class to style your list as table:

```
- Item 1
- Item 2
- Item 3
{.grid-list}
```
will generate:

- Item 1
- Item 2
- Item 3
{.grid-list}

### Images

Easily add a subtle shadow (`decor-shadow`), an outline (`decor-outline`) or round borders (`radius-N`) to your images:

```markdown
![Caption](/your-image.png){.decor-shadow}
![Caption](/your-image.png){.decor-outline}
![Caption](/your-image.png){.radius-7}

![Caption](/your-image.png){.decor-shadow .radius-4}
```

The radius class accepts any value between `0` and `25`. The radius is formatted as pixel units.

## Markdown Reference

Click the help circle icon at the bottom left of the Markdown Editor to display a quick Markdown reference as well as keyboard shortcuts you can use inside the editor:

![beta147-markdownhelp.png](/assets/release-notes/beta147-markdownhelp.png =1000x510){.decor-shadow .radius-4}

## Basic Breadcrumbs

A basic breadcrumb navigation mirroring the current path is now displayed. An improved version with built-in navigation across page at the same level and with actual page titles will be released in a future build.

## Health Endpoint

The endpoint `/healthz` is now available for use by monitoring services (such as load balancers, uptime monitors, etc.).

## Bug fixes / Minor Improvements

- **Fixed:** Interpolation tags are no longer being compiled when displaying a page ([#848](https://github.com/Requarks/wiki/issues/848))
- **Fixed:** Infinite login redirect on the homepage
- **Fixed:** Bug where a page would display intermittently on subsequent load ([#832](https://github.com/Requarks/wiki/issues/832))
- **Fixed:** Menus being covered by the header in Safari ([#834](https://github.com/Requarks/wiki/issues/834))
- **Fixed:** Mobile display in the editor + source view
- **Improvements:** General UI enhancements

## Links

- [Installation](/install)
- [Upgrade from previous Beta (Build 115)](/install/upgrade)

Consider supporting this project by [becoming a Patron](https://www.patreon.com/requarks) or donating to our [Open Collective](https://opencollective.com/wikijs).

# 2.0.0-beta.115

> Released on **April 28th, 2019**
{.is-info}

## Social + Enterprise Authentication

This build comes bundled with 11 social / enterprise authentication modules in addition to local authentication. This is already more than v1 and we're just getting started. The new modules are:

- Auth0
- Discord
- Dropbox
- Facebook
- GitHub
- Google
- LDAP / ActiveDirectory
- Okta
- SAML 2.0
- Slack
- Twitch

More modules (such as Azure AD, CAS, Firebase, Microsoft and generic OAuth2 / OpenID) will come in future betas.

The admin UI for managing auth modules has also been revamped to be easier to use, without having to go back and forth between tabs.

## Bug fixes / Minor improvements
- Handle Git basic auth URI format with or without protocol
- Timeout indicator animation for alerts
- Auth token now refreshes correctly when the short refresh expires
- Attempting to create a page from reserved paths is now blocked
- General UI improvements

## Links

- [Installation](/install)
- [Upgrade from previous Beta (Build 91)](/install/upgrade)

Consider supporting this project by [becoming a Patron](https://www.patreon.com/requarks) or donating to our [Open Collective](https://opencollective.com/wikijs).

# 2.0.0-beta.91

> Released on **April 7th, 2019**
{.is-info}

## Git storage module is now feature complete

The git module now supports import and export of existing content. If you created content in Wiki.js before enabling the git module, you can now run the **Add Untracked Changes** button to add all content to source control tracking. You can also do the same for the opposite direction; if you have content in your remote repository that isn't yet in the DB, run the **Import Everything** task to import missing content.

One of the most requested feature was the ability to force a manual sync. This is now possible using the **Force Sync** action. Note that you can also specify the interval at which synchronization occurs.

## Local Disk storage module is now feature complete

The Daily Backup option is now working. It creates an gzipped archive of all content currently on disk, every 24h, in a subfolder named `_daily`. Archives are kept for a full month before being overwritten.

You can also manually trigger a backup with the content currently on disk using the **Create Backup** action. The archive will be created in the `_manual` subfolder.

Just like the git module, if you created content before the storage module was activated, you will have missing content on disk. Use the **Dump all content to disk** action to output all content from the DB to disk.

## Bug fixes / Minor improvements
- Removed external dependencies on Google Fonts
- Dockerfile improvements to run as node user + apk install fix
- The Pages admin section is now listing all pages. (wip)
- The Insert Image overlay UI can now be displayed, but not functional yet. (wip)

## Links

- [Installation](/install)
- [Upgrade from previous Beta (Build 84)](/install/upgrade)

Consider supporting this project by [becoming a Patron](https://www.patreon.com/requarks) or donating to our [Open Collective](https://opencollective.com/wikijs).

# 2.0.0-beta.84

> Released on **March 24th, 2019**
{.is-info}

## Additional Search Engines
This release includes 2 new search engines:

- Algolia
- Elasticsearch

Check out the [docs](/search) for the setup instructions.

## Bug fixes / Minor improvements
- Fixed error when saving navigation in admin area
- Fixed guest search failing because of missing global permissions
- Fixed PostgreSQL search engine indexing issues
- Improved search suggestions from sanitized content
- Search engine deactivate handler is now being called on engine switch
- Markdown editor UI improvements for insert actions (wip)

## Breaking Changes

> If you are using, or have used the PostgreSQL search engine at least once in the past, you must follow the following procedures to recreate the index tables correctly:
{.is-danger}

1. Make sure the **Database - PostgreSQL** search engine is enabled. Select it and click **Apply** if that's not already the case.
2. Select the **Database - Basic** search engine and click **Apply**. This will trigger the deactivation procedure for the PostgreSQL engine, effectively dropping the index tables.
3. Select the **Database - ProgreSQL** search engine again and click **Apply**. This will recreate the index tables correctly.
4. Finally, click **Rebuild Index** to add all existing content to the index.

## Links

- [Installation](/install)
- [Upgrade from previous Beta (Build 68)](/install/upgrade)

Consider supporting this project by [becoming a Patron](https://www.patreon.com/requarks) or donating to our [Open Collective](https://opencollective.com/wikijs).

# 2.0.0-beta.68

> Released on **March 17th, 2019**
{.is-info}

## Search
Search is now available in this build! Start typing in the search bar to quickly find your pages. This release includes 4 engines:

- Azure Search
- AWS CloudSearch
- DB - Basic
- DB - PostgreSQL

Check out the [docs](/search) for the setup instructions.

![Search Results](/assets/release-notes/beta68-searchresults.png =1000x){.decor-shadow .radius-4}

## SQLite Support
SQLite is now supported and will no longer throw an error during setup. This brings to 5 the number of supported database engines!

## Git Change Processing
Any changes made in the remote git repository will now be picked up and reflected in the wiki. Note that any pages created before enabling Git will not be pushed to the remote repository. This will be addressed in an upcoming release. In the meantime, simply saving the page again fixes this issue.

## HTTP to HTTPS Redirect
You can now listen on HTTP and redirect all requests to HTTPS as an option. See the SSL section in the `config.sample.yml` file.

## Bug fixes / Minor improvements
- Fixed HTTPS server crash
- Show last sync date in Storage status panel
- Dedicated Dev Flags page in Admin area

## Links

- [Installation](/install)
- [Upgrade from previous Beta (Build 42)](/install/upgrade)

Consider supporting this project by [becoming a Patron](https://www.patreon.com/requarks) or donating to our [Open Collective](https://opencollective.com/wikijs).

# 2.0.0-beta.42

> Released on **February 20th, 2019**
{.is-info}

## MySQL, MariaDB and MSSQL support
The initial beta had issues with DBs that were not PostgreSQL. This is now fixed. MariaDB, MySQL, MSSQL and PostgreSQL are now fully supported. Note that SQLite requires some more development and should be working in the next beta!

## Redis is no longer necessary
The Redis requirement has been removed. You now only need a database to run Wiki.js! Redis ended up not being used enough to warrant having it as a dependency. The few parts that were relying on it were re-engineered to use in-memory mechanisms instead.

## Delete Page feature
You can now delete any page from the dropdown menu found at the top left of the page (if you have access). Even though the history feature is not yet available, deleted pages are still kept in the DB and you'll be able to restore them when the feature is ready!.

## Theme Code Injection (CSS/JS)
You can now inject your own CSS or Javascript tags in all pages of your wiki from the **Administration Area**. Located in the **Themes** section, use the CSS Override, Head HTML Injection or Body HTML Injection fields to insert your code.

## Local disk + Git integration *(work in progress)*
The **Local File System** and **Git** storage module are now available for use.

The **Local File System** module simply writes content as files on the local disk. Note that the daily backups option is not yet working. This module is limited to push synchronization only for now, meaning it won't pick up changes made outside Wiki.js.

The **Git** module offers full integration with remote Git repositories (as found in v1). However, v2 goes a step further and is more resilient to various configurations. For example, you can now use an uninitialized repository or specify a branch other than master. While all synchronization options are planned for this module, this beta is limited to the push operations only. You can still choose Sync (default) or Pull when configuring the module, but any changes made outside Wiki.js will not be picked up. Additionally, existing pages will not be pushed until you save them again from the editor. Full functionality is expected for the next beta!

## HTTPS Support
Due to popular request, Wiki.js can now listen on the HTTPS port with your own SSL certificates, eliminating the need for a reverse proxy for most scenarios. Look at the [sample config.yml](https://github.com/Requarks/wiki/blob/2.0.0-beta.42/config.sample.yml#L53-L67) for all possible options. Note that if you're using Docker, you'll need to mount your own config.yml file as the HTTPS options are not yet available as environment variables.

## Many bug fixes...
- Fixed root admin refresh token fail
- Fixed error page metadata title warning
- Fixed telemetry
- Await page render job to complete before resolving
- Added rate limiting to login mutations
- Moved Insert Media button in Markdown editor
- Use semver for DB migrations ordering
- Dev locale .yml files in `server/locales` are now loaded

## Links

- [Installation](/install)
- [Upgrade from previous Beta (Build 11)](/install/upgrade)

Consider supporting this project by [becoming a Patron](https://www.patreon.com/requarks) or donating to our [Open Collective](https://opencollective.com/wikijs).

# 2.0.0-beta.11

> Released on **January 20th, 2019**
{.is-info}

- Initial Beta Release

![](https://a.icons8.com/TbNanZXe/g4MdL9/svg.svg){.align-abstopright}