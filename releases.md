---
title: Release Notes
description: List of new features, bug fixes and improvements
published: true
date: 2020-03-22T23:50:21.303Z
tags: 
---

- [Current Development Roadmap *View the tasks currently being worked on and their status for the next release.*](/releases/current)
- [Future Releases Roadmap *Learn about long term plans and future major releases.*](/releases/future)
- [FAQ / Questions *Where's the detailed timeline? When is feature X being released?*](/releases/about)
{.links-list}

# Upcoming - 2.2

> This build is **under active development** and has not yet been released.
> **ETA: March 2020**
{.is-warning}

## Major Features
- Page History
	- Compare 2 versions
  - View version source
  - Download version
  - Restore version
  - Branch off version
- Create / Manage API Keys
- Save Conflict Detection + Compare Screen
- Content License option for the footer

## Bug fixes / Minor Improvements

- **Fixed:** Apply request increased body limit to GraphQL ([#1480](https://github.com/Requarks/wiki/issues/1480))
- **Fixed:** Hide sidebar on smaller screen and auto-detect on resize.
- **Fixed:** Delete User Keys when deleting a User ([#1586](https://github.com/Requarks/wiki/issues/1586))
- **Fixed:** XML-like tags in code blocks now render correctly as code ([#1559](https://github.com/Requarks/wiki/issues/1559))
- **Fixed:** Task lists are now rendered correctly with HTML Sanitization enabled.
- **Fixed:** `figcaption` and `details` tags are now rendered correctly with HTML Sanitization enabled ([#1542](https://github.com/Requarks/wiki/issues/1542))
- **Fixed:** KaTeX expressions are now rendered correctly with HTML Sanitization enabled ([#1566](https://github.com/Requarks/wiki/issues/1566))
- **Fixed:** Twitch module is now using the latest OAuth method ([#1561](https://github.com/Requarks/wiki/issues/1561))
- **Fixed:** Toggling the preview panel in markdown no longer results in unstyled code blocks ([#1484](https://github.com/Requarks/wiki/issues/1484))
- **Improvements:** KaTeX expressions are now rendered in the Preview panel.
- **Improvements:** Option to open all External Links in New Tab ([#1453](https://github.com/Requarks/wiki/issues/1453))
- **Improvements:** Show Save button as Saved when no content is modified.
- **Improvements:** Edit Title from header in Editors.
- **Improvements:** Twemoji images are now loaded locally instead of MaxCDN.
- **Improvements:** Remote development in VS Code is now supported and is now the preferred development environment ([#1533](https://github.com/Requarks/wiki/issues/1533))
- **Improvements:** Option to restrict Discord authentication to a specific server ([#1548](https://github.com/Requarks/wiki/issues/1548))

# 2.1.113

> Released on **February 14th, 2020**
{.is-info}

## Major Features

- Azure Blob Storage Module
- Delete / Deactivate a User
- Integrate ARM64 & ARMv7 images into standard build pipeline
- LaTeX expressions rendering (KaTeX module)
- Let's Encrypt Built-In Support
- Manage / Delete Tags
- Manually verify a User
- Page Rules for matching Tags ([#1418](https://github.com/Requarks/wiki/issues/1418))
- Save Rendering Configuration
- SFTP Storage Module
- Social Sharing Menu
- Specify a Custom Logo
- Tags Autocomplete in Page Properties
- Utility - Re-render all pages
- Visualize Pages (Hierarchical Tree, Hierarchical Radial & Relational Radial)

## Bug fixes / Minor Improvements

- **Fixed:** Search results are not paginated. ([#942](https://github.com/Requarks/wiki/issues/942))
- **Fixed:** PostgreSQL search query now uses the configured locale ([#1269](https://github.com/Requarks/wiki/issues/1269))
- **Fixed:** Nested lists bullets native implementation ([#1283](https://github.com/Requarks/wiki/issues/1283))
- **Fixed:** Truncate picture URL from 3rd-party auth strategy when too long ([#1311](https://github.com/Requarks/wiki/issues/1311))
- **Fixed:** Vuetify offset bug in RTL layouts ([#1326](https://github.com/Requarks/wiki/issues/1326))
- **Fixed:** Missing indentation in nested lists for RTL layouts ([#1327](https://github.com/Requarks/wiki/issues/1327))
- **Fixed:** View source is now using `read:source` permission ([#1388](https://github.com/Requarks/wiki/issues/1388))
- **Fixed:** Hide new page button when path is not available. ([#1394](https://github.com/Requarks/wiki/issues/1394))
- **Fixed:** List formatting multiline with fancy bullets. ([#1406](https://github.com/Requarks/wiki/issues/1406))
- **Fixed:** Page Rules roles are now validated per rule. ([#1447](https://github.com/Requarks/wiki/issues/1447))
- **Fixed:** Markdown editor now reflects the proper direction in RTL layouts.
- **Fixed:** Non-pages internal links being detected as invalid pages on subsequent finds.
- **Fixed:** Page History content column field is migrated to LONGTEXT for MySQL/MariaDB and MS SQL Server.
- **Fixed:** SRI is now disabled at build time. *To be reintroduced when a proper solution for turning it on/off is found.*
- **Fixed:** Redirect login page from home page only if user is guest.
- **Improvements:** Accept custom SSL configuration for database connection using PostgreSQL, MySQL and MariaDB.
- **Improvements:** Admin Pages are now sorted by last updated by default ([#1271](https://github.com/Requarks/wiki/issues/1271))
- **Improvements:** An Export All action has been added to the AWS S3 storage module.
- **Improvements:** Automatically redirect to previous path after login.
- **Improvements:** Backers from Patreon and GitHub Sponsors are now displayed in the Contribute admin section.
- **Improvements:** Clear new password field in Admin User edit upon saving.
- **Improvements:** Code Injection fields under Admin Theme are now using monospaced font.
- **Improvements:** CSS Injection content is now automatically beautified in the Admin area.
- **Improvements:** Display detailed error when db connection fails using pg driver.
- **Improvements:** Git Local Repository can now be purged and reinitialized from the admin.
- **Improvements:** Git Connection SSH port can now be overriden. ([#1432](https://github.com/Requarks/wiki/issues/1432))
- **Improvements:** In the editor, <kbd>CTRL</kbd> + Click the save button will automatically close the editor upon saving.
- **Improvements:** Predefine `/wiki/data/content` as a volume with `node:node` permissions in Dockerfile. ([#1288](https://github.com/Requarks/wiki/issues/1288))
- **Improvements:** Redirect to a page by its internal ID using path `/i/123`, only with read permissions.

## Links

- [Installation](/install)
- [Upgrade from 2.0.12](/install/upgrade)
- [Migrate from 1.x](/install/migrate)

Consider supporting this project by [becoming a GitHub Sponsor](https://github.com/sponsors/NGPixel), [becoming a Patron](https://www.patreon.com/requarks) or donating to our [Open Collective](https://opencollective.com/wikijs).

# 2.0.12

> Released on **November 23rd, 2019**
{.is-info}

## Bug fixes / Minor Improvements

- **Fixed:** Long Code blocks are no longer incorrectly broken into multiple lines ([#1079](https://github.com/Requarks/wiki/issues/1079))
- **Fixed:** Markdown preview fails to load lang files for code blocks ([#1162](https://github.com/Requarks/wiki/issues/1162))
- **Fixed:** Markdown help dialog shown below editor ([#1164](https://github.com/Requarks/wiki/issues/1164))
- **Fixed:** PostgreSQL search engine error during page move ([#1181](https://github.com/Requarks/wiki/issues/1181))
- **Fixed:** Exclude assets from internal link detection during render ([#1189](https://github.com/Requarks/wiki/issues/1189))
- **Fixed:** Use HTTPS for PlantUML default server value ([#1223](https://github.com/Requarks/wiki/issues/1223))
- **Fixed:** Handle email verification exceptions ([#1227](https://github.com/Requarks/wiki/issues/1227))
- **Fixed:** Missing write:pages permission for editing existing pages ([#1228](https://github.com/Requarks/wiki/issues/1228))
- **Fixed:** Vertical page title positioning in Safari ([#1233](https://github.com/Requarks/wiki/issues/1233))
- **Fixed:** Allow target property in markdown attributes ([#1240](https://github.com/Requarks/wiki/issues/1240))
- **Fixed:** Search hint display no results found error when empty ([#1255](https://github.com/Requarks/wiki/issues/1255))
- **Improvements:** A copy button now appears on mouse-over of code blocks.

## Links

- [Installation](/install)
- [Upgrade from 2.0.1 / RC / Beta](/install/upgrade)
- [Migrate from 1.x](/install/migrate)

Consider supporting this project by [becoming a GitHub Sponsor](https://github.com/sponsors/NGPixel), [becoming a Patron](https://www.patreon.com/requarks) or donating to our [Open Collective](https://opencollective.com/wikijs).

# 2.0.1

> Released on **November 17th, 2019**
{.is-info}

- Initial Stable release :tada:

## Bug fixes / Minor Improvements

- **Fixed:** Search UI would hang when pressing enter before results ([#1086](https://github.com/Requarks/wiki/issues/1086))
- **Fixed:** Nested Lists padding and spacing ([#1114](https://github.com/Requarks/wiki/issues/1114))
- **Fixed:** Remove explicit ids for groups and users during setup ([#1156](https://github.com/Requarks/wiki/issues/1156))
- **Fixed:** HTML tags are now properly transformed into spaces for search analysis ([#1160](https://github.com/Requarks/wiki/issues/1160))
- **Fixed:** Locale is no longer prefixed to links when using system links ([#1165](https://github.com/Requarks/wiki/issues/1165))
- **Fixed:** Locale is no longer prefixed to links when namespacing is off ([#1166](https://github.com/Requarks/wiki/issues/1166))
- **Fixed:** Missing right padding on blockquotes ([#1168](https://github.com/Requarks/wiki/issues/1168))
- **Fixed:** Handle link reformatting from home path ([#1169](https://github.com/Requarks/wiki/issues/1169))
- **Fixed:** Exclude non-class attributes from markdown rendering ([#1174](https://github.com/Requarks/wiki/issues/1174))
- **Fixed:** Cannot update user email from admin ([#1197](https://github.com/Requarks/wiki/issues/1197))
- **Fixed:** Non-image assets are now inserted correctly in the Visual Editor ([#1207](https://github.com/Requarks/wiki/issues/1207))
- **Fixed:** Git Private Key is now handled correctly when ending LF is missing ([#1209](https://github.com/Requarks/wiki/issues/1209))
- **Fixed:** Marker Highlighting is now shown correctly on rendered pages
- **Improvements:** Text is now selectable in Admin - System Info ([#1161](https://github.com/Requarks/wiki/issues/1161))
- **Improvements:** Extended twemoji country flags support ([#1163](https://github.com/Requarks/wiki/issues/1163))
- **Improvements:** Edit Group tab UI ([#1218](https://github.com/Requarks/wiki/issues/1218))
- **Miscellaneous:** Stable DB migration + beta migration to stable

## Links

- [Installation](/install)
- [Upgrade from previous RC / Beta](/install/upgrade)
- [Migrate from 1.x](/install/migrate)

Consider supporting this project by [becoming a GitHub Sponsor](https://github.com/sponsors/NGPixel), [becoming a Patron](https://www.patreon.com/requarks) or donating to our [Open Collective](https://opencollective.com/wikijs).

# 2.0.0-rc.17

> Released on **October 27th, 2019**
{.is-info}

## Bug fixes / Minor Improvements

- **Fixed:** Breadcrumbs links on 3rd level or higher are now processed correctly ([#930](https://github.com/Requarks/wiki/issues/930))
- **Fixed:** Azure AD will now fallback to preferred_username if email field is missing ([#1050](https://github.com/Requarks/wiki/issues/1050))
- **Fixed:** Nested lists are now indented correctly ([#1114](https://github.com/Requarks/wiki/issues/1114))
- **Fixed:** Page delete no longer produce a pageTree foreign key error ([#1119](https://github.com/Requarks/wiki/issues/1119))
- **Fixed:** MSSQL setup, pageTree, page delete, asset folders queries are now working ([#1125](https://github.com/Requarks/wiki/issues/1125), [#1141](https://github.com/Requarks/wiki/issues/1141))
- **Fixed:** Table of Contents go-to header is now working for all editors ([#1127](https://github.com/Requarks/wiki/issues/1127))
- **Fixed:** Analytics modules var replace is now made globally ([#1129](https://github.com/Requarks/wiki/issues/1129))
- **Fixed:** Tags are now exported and imported during storage events ([#1149](https://github.com/Requarks/wiki/issues/1149))
- **Fixed:** Setup retries now correctly reset the table IDs to 0
- **Improvements:** dataPath variable can now be specified as the data folder location in config.yml ([#1118](https://github.com/Requarks/wiki/issues/1118))

## Links

- [Installation](/install)
- [Upgrade from previous RC / Beta](/install/upgrade)

Consider supporting this project by [becoming a GitHub Sponsor](https://github.com/sponsors/NGPixel), [becoming a Patron](https://www.patreon.com/requarks) or donating to our [Open Collective](https://opencollective.com/wikijs).

# 2.0.0-rc.1

> Released on **October 20th, 2019**
{.is-info}

## Migration Tool from Wiki.js 1.x

It's now possible to migrate content, uploads and users from a Wiki.js 1.x installation using a quick easy to use tool.

## Assets Export/Import for Storage Modules

Assets are now exported / imported from storage modules alongside the pages.

## Move / Rename a Page

You can now move or rename an existing page, both from a dedicated move dialog or when editing a page through the Page Properties dialog. It's also possible to move pages across locales.

## Page Selector

It's now possible to see the full structure of your wiki when creating a new page or moving an existing page.

## Automated Upgrade for Docker installations

Wiki.js can now upgrade itself to the latest version when using the Dockerized version and a companion docker agent. This will be the default in the upcoming DigitalOcean Marketplace image. *More information coming soon.*

## Raw HTML Code Editor

A basic code editor for raw HTML is now available.

## PlantUML diagrams in the Markdown Editor

You can now include PlantUML diagrams from the Markdown Editor. Thanks to [@ethanmdavidson](https://github.com/ethanmdavidson).

Example:
```
@startuml
participant User

User -> A: DoWork
activate A #FFBBBB

A -> A: Internal call
activate A #DarkSalmon

A -> B: << createRequest >>
activate B

B --> A: RequestCreated
deactivate B
deactivate A
A -> User: Done
deactivate A

@enduml
```

@startuml
participant User

User -> A: DoWork
activate A #FFBBBB

A -> A: Internal call
activate A #DarkSalmon

A -> B: << createRequest >>
activate B

B --> A: RequestCreated
deactivate B
deactivate A
A -> User: Done
deactivate A

@enduml

## Bug fixes / Minor Improvements

- **Fixed:** Selection in search results is now readable with dark mode enabled.
- **Fixed:** Git Actions no longer crash at missing getFileExtension method ([#1040](https://github.com/Requarks/wiki/issues/1040))
- **Fixed:** Ignore mailto links from link processing ([#1041](https://github.com/Requarks/wiki/issues/1041))
- **Fixed:** Restore Unicode chars from render for search content ([#1043](https://github.com/Requarks/wiki/issues/1043))
- **Fixed:** Display Admin Link for all admin permissions ([#1052](https://github.com/Requarks/wiki/issues/1052))
- **Fixed:** Replace mail password unless changed in Admin Mail settings ([#1053](https://github.com/Requarks/wiki/issues/1053))
- **Fixed:** System users and groups are now set a fixed ID during setup ([#1056](https://github.com/Requarks/wiki/issues/1056))
- **Fixed:** Removed per-item upload process which would always upload to root folder ([#1058](https://github.com/Requarks/wiki/issues/1058))
- **Fixed:** 5-letters locales are now loaded properly ([#1062](https://github.com/Requarks/wiki/issues/1062))
- **Fixed:** Code blocks are now readable in print view ([#1068](https://github.com/Requarks/wiki/issues/1068))
- **Fixed:** Prevent duplicate group assignment ([#1081](https://github.com/Requarks/wiki/issues/1081))
- **Fixed:** Removing a Page Rule now deletes the correct one ([#1083](https://github.com/Requarks/wiki/issues/1083))
- **Fixed:** Admin Navigation drag-n-drop dependency update ([#1085](https://github.com/Requarks/wiki/issues/1085))
- **Fixed:** Groups Delete dialog is now triggered properly ([#1009](https://github.com/Requarks/wiki/issues/1009), [#1088](https://github.com/Requarks/wiki/issues/1088))
- **Fixed:** Page mutations are now checked against the group page rules in addition to global permissions.
- **Improvements:** The X-Forwarded-* headers can now be trusted / ignored from the admin UI.
- **Improvements:** The SRI hash for CSS/JS resources can now be enabled / disabled from the admin UI.
- **Improvements:** Support for DB_PASS_FILE env variable for Docker Secret file.
- **Improvements:** Support for CONFIG_FILE env variable for specifying a custom path for the config file.
- **Improvements:** Baidu Tongji analytics module is now available ([#1087](https://github.com/Requarks/wiki/pull/1087))

## Links

- [Installation](/install)
- [Upgrade from previous Beta (Build 303)](/install/upgrade)

Consider supporting this project by [becoming a GitHub Sponsor](https://github.com/sponsors/NGPixel), [becoming a Patron](https://www.patreon.com/requarks) or donating to our [Open Collective](https://opencollective.com/wikijs).

# Previous Releases

- [2.0 Beta Releases](/releases-beta)