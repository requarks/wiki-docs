---
title: Previous Stable Releases
description: List of new features, bug fixes and improvements
published: true
date: 2021-04-26T15:55:00.810Z
tags: 
editor: markdown
dateCreated: 2021-04-26T15:54:07.425Z
---

# 2.4.107

> Initially released on **June 5th, 2020** as `2.4.105`.
> Hotfix `2.4.107` was released on **June 14th, 2020**.
> Users that upgraded to versions `2.4.105` should upgrade immediately to `2.4.107`.
{.is-info}

### Hotfix 1 *(2.4.107)*{.caption}
- The plain blockquote icon is now a quote icon instead of an info symbol.
- Added Generic S3 Storage Module
- **Fixed:** Prevent mustache template injection bypass via encoded/unencoded root level text elements ([GHSA-9jgg-4xj2-vjjj](https://github.com/Requarks/wiki/security/advisories/GHSA-9jgg-4xj2-vjjj))
- **Fixed:** Listing assets are now validated against the `read:assets` permission. ([#1928](https://github.com/Requarks/wiki/issues/1928))
- **Fixed:** Target attribute is no longer stripped by the HTML Security module. ([#2012](https://github.com/Requarks/wiki/issues/2012))
- **Fixed:** Sidebar is no longer empty when the JWT is expired ([#2037](https://github.com/Requarks/wiki/issues/2037))

### Major Features *(2.4.105)*{.caption}

- Comments
	- Commento
  - Default (native)
  - Disqus
- Content Tabs
- Create New Page from Template
- Cypress E2E testing added to CI pipeline for all 5 DB engines.
- Kroki Rendering Module ([#1900](https://github.com/Requarks/wiki/issues/1900))
- MathJax Rendering Module
- PlantUML live rendering in Markdown preview
- Timezone, Date Format and Appearance (light/dark) per User Profile
- Upload limits configuration from the Administration area

### Minor Improvements *(2.4.105)*{.caption}

- Added a Static Navigation only option for navigation *(pre-2.3 display)*.
- Added help links to administration are Modules sections.
- Added option for navigation links to open in a new window.
- Added rel option for external content links for increased XSS security.
- Added target user option when deleting a user with content.
- Admin Users list now shows active/disabled indicator + last login date.
- Assets (js, css, svg, fonts, etc.) have been relocated to subdirectory _assets.
- Blockquotes now have a built-in icon + color margin for increased visibility.
- Certificate verification can now be disabled in Mail settings.
- Dev Docker-Compose improvements and cleanup. ([#1905](https://github.com/Requarks/wiki/issues/1905))
- DOMPurify is now used instead of the xss module as the HTML sanitizer.
- Elasticsearch can now do partial match by default. ([#1882](https://github.com/Requarks/wiki/issues/1882))
- New Extensions section in the administration area. *(WIP)*
- Page TOC is now sticky during scroll.
- Setup success screen now display a confetti animation!
- Pages Visualization diagram can now be zoomed and panned.
- Twemoji assets are now packaged as an ASAR archive, significantly reducing file count + dev compilation time.

### Bug fixes *(2.4.105)*{.caption}

- **Fixed:** CKEditor (Visual Editor) now handles RTL locales correctly. ([#1636](https://github.com/Requarks/wiki/issues/1636))
- **Fixed:** Roboto-Mono font is now fetched properly when using Arabic. ([#1708](https://github.com/Requarks/wiki/issues/1708))
- **Fixed:** Long words are now broken into multiple lines in Markdown editor. ([#1743](https://github.com/Requarks/wiki/issues/1743))
- **Fixed:** Removed the extra `)` added to some links in Visual Editor. ([#1788](https://github.com/Requarks/wiki/issues/1788))
- **Fixed:** HTML from Visual Editor is now beautified before saving for proper diff versioning. ([#1804](https://github.com/Requarks/wiki/issues/1804))
- **Fixed:** Markdown Footnotes IDs are no longer stripped by HTML Sanitization module. ([#1819](https://github.com/Requarks/wiki/issues/1819))
- **Fixed:** Saved state is now updated for page properties. ([#1826](https://github.com/Requarks/wiki/issues/1826))
- **Fixed:** Anchor scrolling will now handle image loading offset correctly after load. ([#1870](https://github.com/Requarks/wiki/issues/1870))
- **Fixed:** Removed unsuitable font for Persian language. ([#1871](https://github.com/Requarks/wiki/issues/1871))
- **Fixed:** Font Awesome icons are now sized correctly in the sidebar. ([#1887](https://github.com/Requarks/wiki/issues/1887))
- **Fixed:** Keycloak module is now using fullname field with username fallback. ([#1888](https://github.com/Requarks/wiki/issues/1888))
- **Fixed:** Bullet list markers in RTL mode are now aligned correctly. ([#1892](https://github.com/Requarks/wiki/issues/1892))
- **Fixed:** Search progress bar is no longer shown when exiting ([#1912](https://github.com/Requarks/wiki/issues/1912))
- **Fixed:** Some Pages Visualization tree nodes were not sorted correctly and would display the wrong title. ([#1914](https://github.com/Requarks/wiki/issues/1914))
- **Fixed:** S3 Export All is triggered correctly. ([#1922](https://github.com/Requarks/wiki/issues/1922))
- **Fixed:** Links to subtitles with special characters are now decoded correctly. ([#1949](https://github.com/Requarks/wiki/issues/1949))
- **Fixed:** Android + iOS favicons are now referenced correctly. ([#1959](https://github.com/Requarks/wiki/issues/1959), [#1965](https://github.com/Requarks/wiki/issues/1965))
- **Fixed:** Open Redirect Vulnerability mitigation. ([#1963](https://github.com/Requarks/wiki/issues/1963))
- **Fixed:** An invalid LDAP configuration no longer prevent the local auth module from initializing. ([#1978](https://github.com/Requarks/wiki/issues/1978))
- **Fixed:** Proper image floating alignment when using Visual Editor ([#1981](https://github.com/Requarks/wiki/issues/1981))
- **Fixed:** Page paths starting with a slash are now stripped correctly ([#1982](https://github.com/Requarks/wiki/issues/1982))
- **Fixed:** Added missing directory page to the browse sidebar menu.
- **Fixed:** Write permissions can no longer be selected for the Guest group.
- **Fixed:** Semver is now used to determine if latest version is more recent than currently installed version.
- **Fixed:** Legacy (IE11) page view is now displayed correctly.

### Links

- [Installation](/install)
- [Upgrade from 2.3.81](/install/upgrade)
- [Migrate from 1.x](/install/migrate)

Consider supporting this project by [becoming a GitHub Sponsor](https://github.com/sponsors/NGPixel), [becoming a Patron](https://www.patreon.com/requarks) or donating to our [Open Collective](https://opencollective.com/wikijs).

# 2.3.81

> Initially released on **April 24th, 2020** as `2.3.71-73`.
> Hotfix `2.3.77` was released on **April 25th, 2020**.
> Hotfix `2.3.81` was released on **May 1st, 2020**.
> Users that upgraded to versions `< 2.3.81` should upgrade immediately to `2.3.81`.
{.is-info}

### Hotfix 2 *(2.3.81)*{.caption}
- **Fixed:** Sanitize HTML in Preview panel of the Markdown Editor ([GHSA-vj72-c9vq-qxrv](https://github.com/Requarks/wiki/security/advisories/GHSA-vj72-c9vq-qxrv))

### Hotfix 1 *(2.3.77)*{.caption}
- Added option to copy navigation items from other locale ([#1774](https://github.com/Requarks/wiki/issues/1774))
- **Fixed:** Navigation mode is now persisted correctly ([#1776](https://github.com/Requarks/wiki/issues/1776))
- **Fixed:** Git SSH port is no longer explictly defined ([#1777](https://github.com/Requarks/wiki/issues/1777))

### Major Features *(2.3.71)*{.caption}

- Updated Navigation
	- 3 Navigation Modes: Tree, Mixed or None
	- Tree-based Navigation
  - Permission-based Navigation
- Duplicate Page
- Support for Chemical Equations in KaTeX
- Support for Mermaid diagrams
- User Profile / Account Management
	- Change Account Info
  - Change Password *(local authentication only)*
  - List of Groups user is part of
  - Activity Panel
  - Pages user created / last modified
- Link Autocomplete in Markdown editor
- Insert Link Dialog
- High Availability Support *(event propagation across instances)*:
	- Delete Page Cache
  - Flush Cache
  - Reload Group Permissions
  - Reload Auth Strategies
  - Reload API Keys
  - Reload Config
  
### Minor Improvements *(2.3.71)*{.caption}

- Replace GA with hosted graph telemetry.
- PlantUML default enclosing markers are now ` ```plantuml ` and ` ``` `
- View the last login date of any user in Administration Area
- Tags selector in Page Properties no longer remove tags on backspace and new tags automatically empty the field.
- Added `DB_SSL_CA` env variable to pass the CA certificate as a single-line value.
- Added option in LDAP authentication module to disable TLS certificate validation.

### Bug fixes *(2.3.71)*{.caption}

- **Fixed:** MSSQL + MariaDB (older versions) migrations 2.2.17 are now executing correctly ([#1610](https://github.com/Requarks/wiki/issues/1610), [#1642](https://github.com/Requarks/wiki/issues/1642))
- **Fixed:** Tags are now always normalized and trimmed ([#1364](https://github.com/Requarks/wiki/issues/1364))
- **Fixed:** Footer is now shown in print view ([#1593](https://github.com/Requarks/wiki/issues/1593))
- **Fixed:** Print view now displays content past the second page ([#1034](https://github.com/Requarks/wiki/issues/1034))
- **Fixed:** User/Pass are now URI-encoded in HTTPS git remotes ([#1709](https://github.com/Requarks/wiki/issues/1709))
- **Fixed:** API keys are now automatically reloaded after creation ([#1713](https://github.com/Requarks/wiki/issues/1713))
- **Fixed:** Daily backups are now correctly triggered for Local Disk storage module ([#1714](https://github.com/Requarks/wiki/issues/1714))
- **Fixed:** Add `i` tag + `start` property for `ol` tag to HTML sanitizer whitelist ([#1724](https://github.com/Requarks/wiki/issues/1724))
- **Fixed:** All enabled locales are now available in group page rules ([#1739](https://github.com/Requarks/wiki/issues/1739))
- **Fixed:** Git rename is now performed via rm + add to avoid a bad source error. ([#1750](https://github.com/Requarks/wiki/issues/1750))
- **Fixed:** Icons in Admin Navigation page are now squared, matching the normal pages display. ([#1767](https://github.com/Requarks/wiki/issues/1767))
- **Fixed:** Trailing slashes are now removed automatically when creating a page or during a page move. ([#1769](https://github.com/Requarks/wiki/issues/1769))
- **Fixed:** Guest group is now reloaded immediately on update.
- **Fixed:** Site URL field in Admin > General is now trimmed and trailing-slash removed automatically.
- **Fixed:** Registration form is now displayed correctly in dark mode.

### Links

- [Installation](/install)
- [Upgrade from 2.2.51](/install/upgrade)
- [Migrate from 1.x](/install/migrate)

Consider supporting this project by [becoming a GitHub Sponsor](https://github.com/sponsors/NGPixel), [becoming a Patron](https://www.patreon.com/requarks) or donating to our [Open Collective](https://opencollective.com/wikijs).

# 2.2.51

> Initially released on **March 28th, 2020** as `2.2.50`. An hotfix was released on **March 29th, 2020** for MySQL installations as `2.2.51`.
> If you successfully upgraded to `2.2.50`, you do not need to upgrade to `2.2.51`.
{.is-info}

### Major Features
- Page History
	- Compare 2 versions
  - View version source
  - Download version
  - Restore version
  - Branch off version
- Create / Manage API Keys
- Save Conflict Detection + Compare Screen
- Content License option for the footer

### Minor Improvements

- KaTeX expressions are now rendered in the Preview panel.
- Option to open all External Links in New Tab ([#1453](https://github.com/Requarks/wiki/issues/1453))
- Show Save button as Saved when no content is modified.
- Edit Title from header in Editors.
- Twemoji images are now loaded locally instead of MaxCDN.
- Remote development in VS Code is now supported and is now the preferred development environment ([#1533](https://github.com/Requarks/wiki/issues/1533))
- Option to restrict Discord authentication to a specific server ([#1548](https://github.com/Requarks/wiki/issues/1548))

### Bug fixes

- **Fixed:** Apply request increased body limit to GraphQL ([#1480](https://github.com/Requarks/wiki/issues/1480))
- **Fixed:** Hide sidebar on smaller screen and auto-detect on resize.
- **Fixed:** Delete User Keys when deleting a User ([#1586](https://github.com/Requarks/wiki/issues/1586))
- **Fixed:** XML-like tags in code blocks now render correctly as code ([#1559](https://github.com/Requarks/wiki/issues/1559))
- **Fixed:** Task lists are now rendered correctly with HTML Sanitization enabled.
- **Fixed:** `figcaption` and `details` tags are now rendered correctly with HTML Sanitization enabled ([#1542](https://github.com/Requarks/wiki/issues/1542))
- **Fixed:** KaTeX expressions are now rendered correctly with HTML Sanitization enabled ([#1566](https://github.com/Requarks/wiki/issues/1566))
- **Fixed:** Twitch module is now using the latest OAuth method ([#1561](https://github.com/Requarks/wiki/issues/1561))
- **Fixed:** Toggling the preview panel in markdown no longer results in unstyled code blocks ([#1484](https://github.com/Requarks/wiki/issues/1484))
- **Fixed:** Right-aligned images are now shown above header lines ([#1588](https://github.com/Requarks/wiki/issues/1588))
- **Fixed:** Footnotes are now shown correctly in the Markdown editor preview.
- **Fixed:** Lists are now nested and stacked with proper spacing ([#1609](https://github.com/Requarks/wiki/issues/1609))
- **Fixed:** The page selector dialog no longer displays duplicate items.
- **Fixed:** Saving and close a page no longer results in a permanent loading dialog if an error occurs.

### Links

- [Installation](/install)
- [Upgrade from 2.1.113](/install/upgrade)
- [Migrate from 1.x](/install/migrate)

Consider supporting this project by [becoming a GitHub Sponsor](https://github.com/sponsors/NGPixel), [becoming a Patron](https://www.patreon.com/requarks) or donating to our [Open Collective](https://opencollective.com/wikijs).

# 2.1.113

> Released on **February 14th, 2020**
{.is-info}

### Major Features

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

### Minor Improvements

- Accept custom SSL configuration for database connection using PostgreSQL, MySQL and MariaDB.
- Admin Pages are now sorted by last updated by default ([#1271](https://github.com/Requarks/wiki/issues/1271))
- An Export All action has been added to the AWS S3 storage module.
- Automatically redirect to previous path after login.
- Backers from Patreon and GitHub Sponsors are now displayed in the Contribute admin section.
- Clear new password field in Admin User edit upon saving.
- Code Injection fields under Admin Theme are now using monospaced font.
- CSS Injection content is now automatically beautified in the Admin area.
- Display detailed error when db connection fails using pg driver.
- Git Local Repository can now be purged and reinitialized from the admin.
- Git Connection SSH port can now be overriden. ([#1432](https://github.com/Requarks/wiki/issues/1432))
- In the editor, <kbd>CTRL</kbd> + Click the save button will automatically close the editor upon saving.
- Predefine `/wiki/data/content` as a volume with `node:node` permissions in Dockerfile. ([#1288](https://github.com/Requarks/wiki/issues/1288))
- Redirect to a page by its internal ID using path `/i/123`, only with read permissions.

### Bug fixes

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

### Links

- [Installation](/install)
- [Upgrade from 2.0.12](/install/upgrade)
- [Migrate from 1.x](/install/migrate)

Consider supporting this project by [becoming a GitHub Sponsor](https://github.com/sponsors/NGPixel), [becoming a Patron](https://www.patreon.com/requarks) or donating to our [Open Collective](https://opencollective.com/wikijs).

# 2.0.12

> Released on **November 23rd, 2019**
{.is-info}

### Minor Improvements

- A copy button now appears on mouse-over of code blocks.

### Bug fixes

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

### Links

- [Installation](/install)
- [Upgrade from 2.0.1 / RC / Beta](/install/upgrade)
- [Migrate from 1.x](/install/migrate)

Consider supporting this project by [becoming a GitHub Sponsor](https://github.com/sponsors/NGPixel), [becoming a Patron](https://www.patreon.com/requarks) or donating to our [Open Collective](https://opencollective.com/wikijs).

# 2.0.1

> Released on **November 17th, 2019**
{.is-info}

- Initial Stable release :tada:

### Minor Improvements

- Text is now selectable in Admin - System Info ([#1161](https://github.com/Requarks/wiki/issues/1161))
- Extended twemoji country flags support ([#1163](https://github.com/Requarks/wiki/issues/1163))
- Edit Group tab UI ([#1218](https://github.com/Requarks/wiki/issues/1218))

### Bug fixes

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
- **Miscellaneous:** Stable DB migration + beta migration to stable

### Links

- [Installation](/install)
- [Upgrade from previous RC / Beta](/install/upgrade)
- [Migrate from 1.x](/install/migrate)

Consider supporting this project by [becoming a GitHub Sponsor](https://github.com/sponsors/NGPixel), [becoming a Patron](https://www.patreon.com/requarks) or donating to our [Open Collective](https://opencollective.com/wikijs).

# 2.0.0-rc.17

> Released on **October 27th, 2019**
{.is-info}

### Minor Improvements

- dataPath variable can now be specified as the data folder location in config.yml ([#1118](https://github.com/Requarks/wiki/issues/1118))

### Bug fixes

- **Fixed:** Breadcrumbs links on 3rd level or higher are now processed correctly ([#930](https://github.com/Requarks/wiki/issues/930))
- **Fixed:** Azure AD will now fallback to preferred_username if email field is missing ([#1050](https://github.com/Requarks/wiki/issues/1050))
- **Fixed:** Nested lists are now indented correctly ([#1114](https://github.com/Requarks/wiki/issues/1114))
- **Fixed:** Page delete no longer produce a pageTree foreign key error ([#1119](https://github.com/Requarks/wiki/issues/1119))
- **Fixed:** MSSQL setup, pageTree, page delete, asset folders queries are now working ([#1125](https://github.com/Requarks/wiki/issues/1125), [#1141](https://github.com/Requarks/wiki/issues/1141))
- **Fixed:** Table of Contents go-to header is now working for all editors ([#1127](https://github.com/Requarks/wiki/issues/1127))
- **Fixed:** Analytics modules var replace is now made globally ([#1129](https://github.com/Requarks/wiki/issues/1129))
- **Fixed:** Tags are now exported and imported during storage events ([#1149](https://github.com/Requarks/wiki/issues/1149))
- **Fixed:** Setup retries now correctly reset the table IDs to 0

### Links

- [Installation](/install)
- [Upgrade from previous RC / Beta](/install/upgrade)

Consider supporting this project by [becoming a GitHub Sponsor](https://github.com/sponsors/NGPixel), [becoming a Patron](https://www.patreon.com/requarks) or donating to our [Open Collective](https://opencollective.com/wikijs).

# 2.0.0-rc.1

> Released on **October 20th, 2019**
{.is-info}

### Major Features

#### Migration Tool from Wiki.js 1.x

It's now possible to migrate content, uploads and users from a Wiki.js 1.x installation using a quick easy to use tool.

#### Assets Export/Import for Storage Modules

Assets are now exported / imported from storage modules alongside the pages.

#### Move / Rename a Page

You can now move or rename an existing page, both from a dedicated move dialog or when editing a page through the Page Properties dialog. It's also possible to move pages across locales.

#### Page Selector

It's now possible to see the full structure of your wiki when creating a new page or moving an existing page.

#### Automated Upgrade for Docker installations

Wiki.js can now upgrade itself to the latest version when using the Dockerized version and a companion docker agent. This will be the default in the upcoming DigitalOcean Marketplace image. *More information coming soon.*

#### Raw HTML Code Editor

A basic code editor for raw HTML is now available.

#### PlantUML diagrams in the Markdown Editor

You can now include PlantUML diagrams from the Markdown Editor. Thanks to [@ethanmdavidson](https://github.com/ethanmdavidson).

Example:
````
```plantuml
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
```
````

```plantuml
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

```

### Minor Improvements

- The X-Forwarded-* headers can now be trusted / ignored from the admin UI.
- The SRI hash for CSS/JS resources can now be enabled / disabled from the admin UI.
- Support for DB_PASS_FILE env variable for Docker Secret file.
- Support for CONFIG_FILE env variable for specifying a custom path for the config file.
- Baidu Tongji analytics module is now available ([#1087](https://github.com/Requarks/wiki/pull/1087))

### Bug fixes

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

### Links

- [Installation](/install)
- [Upgrade from previous Beta (Build 303)](/install/upgrade)

Consider supporting this project by [becoming a GitHub Sponsor](https://github.com/sponsors/NGPixel), [becoming a Patron](https://www.patreon.com/requarks) or donating to our [Open Collective](https://opencollective.com/wikijs).