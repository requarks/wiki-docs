---
title: Release Notes
description: List of new features, bug fixes and improvements
published: true
date: 2021-04-26T15:55:51.424Z
tags: 
editor: markdown
dateCreated: 2019-05-26T03:34:27.819Z
---

- [Roadmap *See planned features / improvements for future releases.*](/releases/roadmap)
- [FAQ / Questions *Where's the detailed timeline? When is feature X being released?*](/releases/about)
{.links-list}

# DEV - 3.0

> This build is **under active development** and has not yet been released.
>
> **ETA: Beta planned for Summer 2021 with final release in Fall 2021**
{.is-warning}

See https://blog.js.wiki/news?tag=3.x for latest news about this upcoming release.

# STABLE - 2.5.201

> Initially released on **September 6th, 2020** as `2.5.117`.
> Hotfix 1 - `2.5.126` was released on **September 7th, 2020**.
> Hotfix 2 - `2.5.132` was released on **September 10th, 2020**.
> Hotfix 3 - `2.5.136` was released on **September 12th, 2020**.
> Hotfix 4 - `2.5.144` was released on **September 14th, 2020**.
> Hotfix 5 - `2.5.159` was released on **October 3rd, 2020**.
> Hotfix 6 - `2.5.170` was released on **October 25th, 2020**.
> Hotfix 7 - `2.5.191` was released on **March 13th, 2021**.
> Hotfix 8 - `2.5.197` was released on **March 26th, 2021**.
> Hotfix 9 - `2.5.201` was released on **April 2nd, 2021**.
{.is-info}

### Hotfix 9 *(2.5.201)*{.caption}
- Added page conversion functionality to switch between editors. *(thanks to the Bern University of Applied Sciences for sponsoring the development of this feature)*

### Hotfix 8 *(2.5.197)*{.caption}
- **Fixed:** Login redirect is now working correctly for non-local strategies. ([#3222](https://github.com/Requarks/wiki/issues/3222))
- **Fixed:** HSTS max-age header is no longer undefined. ([#3225](https://github.com/Requarks/wiki/issues/3225))
- **Fixed:** AWS S3 storage is now copying to the correct bucket for renames. ([#3745](https://github.com/Requarks/wiki/issues/3745))
- **Fixed:** CORS is now disabled to prevent cross-origin requests. ([#3056](https://github.com/Requarks/wiki/issues/3056), thanks to [@pylr](https://github.com/pylr))
- **Fixed:** Mustache expressions at root level from Raw HTML editor are now escaped properly. *(thanks to [Mina M. Edwar](http://linkedin.com/in/mina-mohsen-edwar-0a229025))*

### Hotfix 7 *(2.5.191)*{.caption}
- **Fixed:** Stored XSS through code blocks with mustache expressions. ([GHSA-6xx4-m8gx-826r](https://github.com/Requarks/wiki/security/advisories/GHSA-6xx4-m8gx-826r))
- **Fixed:** Code blocks no longer show duplicate characters in print view. ([#2593](https://github.com/Requarks/wiki/issues/2593))
- **Fixed:** Enable passport-azure-ad workaround for SameSite cookies. ([#2567](https://github.com/Requarks/wiki/issues/2567))
- **Fixed:** Logo in emails is now an absolute URL if path is relative. ([#2628](https://github.com/Requarks/wiki/issues/2628))
- **Fixed:** Set autocommit flag for MySQL. ([#2638](https://github.com/Requarks/wiki/issues/2638))
- **Fixed:** Inline Math interpreted as attributes. ([#2645](https://github.com/Requarks/wiki/issues/2645))
- **Fixed:** Improved ElasticSearch configuration + Draw.io display in RTL mode. ([#2647](https://github.com/Requarks/wiki/issues/2647))
- **Fixed:** Special chars in tags are now parsed properly from URL. ([#2748](https://github.com/Requarks/wiki/issues/2748))
- **Fixed:** Set analyzer for ElasticSearch module. ([#2793](https://github.com/Requarks/wiki/issues/2793))
- **Fixed:** Search index is now updated properly when moving pages. ([#2815](https://github.com/Requarks/wiki/issues/2815))
- **Fixed:** `write:scripts` and `write:styles` are now configurable in group permissions. ([#2829](https://github.com/Requarks/wiki/issues/2829))
- **Fixed:** Tree rebuild no longer fails when batches are too large for SQLite. ([#2830](https://github.com/Requarks/wiki/issues/2830))
- **Fixed:** Local Disk + Git modules now matches injectPageMetadata helper behavior. ([#2832](https://github.com/Requarks/wiki/issues/2832))
- **Fixed:** Search results can now be opened in a new tab via middle-click. ([#2919](https://github.com/Requarks/wiki/issues/2919))
- **Fixed:** LDAP auth module no longer incorrectly reads an empty TLS cert file. ([#2980](https://github.com/Requarks/wiki/issues/2980))
- **Fixed:** Storage sync interval is now read from saved settings instead of module data. ([#3003](https://github.com/Requarks/wiki/issues/3003))

### Hotfix 6 *(2.5.170)*{.caption}
- **Fixed:** Unescaped page title in search results. ([GHSA-pgjv-84m7-62q7](https://github.com/Requarks/wiki/security/advisories/GHSA-pgjv-84m7-62q7))
- **Fixed:** Incorrect translation key for comments cancel button. ([#2543](https://github.com/Requarks/wiki/issues/2543))

### Hotfix 5 *(2.5.159)*{.caption}
- Added Rocket.chat authentication module
- **Fixed:** Asset directory traversal with some storage modules. ([GHSA-whpv-5xg2-w527](https://github.com/Requarks/wiki/security/advisories/GHSA-whpv-5xg2-w527))
- **Fixed:** Tabsets tabs can now be scrolled when view is too small. ([#2442](https://github.com/Requarks/wiki/issues/2442))
- **Fixed:** Markdown editor URL autocompletion misbehaving in certain scenarios. ([#2452](https://github.com/Requarks/wiki/issues/2452))
- **Fixed:** Bypass auth redirect cookie when set to homepage. ([#2478](https://github.com/Requarks/wiki/issues/2478))
- **Fixed:** Handle missing extra field during page render. ([#2499](https://github.com/Requarks/wiki/issues/2499))
- **Fixed:** Set enableArithAbort explicit value for tedious driver. ([#2510](https://github.com/Requarks/wiki/issues/2510))
- **Fixed:** Check for email array during processProfile. ([#2515](https://github.com/Requarks/wiki/issues/2515))
- **Fixed:** Updated Matomo integration client code. ([#2526](https://github.com/Requarks/wiki/issues/2526))

### Hotfix 4 *(2.5.144)*{.caption}
- **Fixed:** Security rendering module no longer strips `allow` attribute when iframes are whitelisted. ([#2354](https://github.com/Requarks/wiki/issues/2354))
- **Fixed:** Basic search engine now supports tags permission filtering. ([#2416](https://github.com/Requarks/wiki/issues/2416))
- **Fixed:** Download button for locales is no longer hidden on smaller screens. ([#2429](https://github.com/Requarks/wiki/issues/2429))
- **Fixed:** Custom login backgrounds selected from the upload asset dialog are now set correctly. ([#2437](https://github.com/Requarks/wiki/issues/2437))
- **Fixed:** All strings are now localized on the login page and select page dialog. ([#2438](https://github.com/Requarks/wiki/issues/2438), [#2439](https://github.com/Requarks/wiki/issues/2439))
- **Fixed:** All authentication provider icons are now in their proper color formats. ([#2441](https://github.com/Requarks/wiki/issues/2441))

### Hotfix 3 *(2.5.136)*{.caption}
- **Fixed:** Draw-io diagrams with texts linebreaks are no longer removed. ([#2415](https://github.com/Requarks/wiki/issues/2415))
- **Fixed:** Admins with `manage:system` are longer blocked from editing / assign users to elevated groups. ([#2424](https://github.com/Requarks/wiki/issues/2378))
- **Fixed:** API requests no longer fail / timeout due to token revalidation. ([#2426](https://github.com/Requarks/wiki/issues/2426))

### Hotfix 2 *(2.5.132)*{.caption}
- **Fixed:** Users with `write:groups` permission can no longer self-promote their group to admin. ([#2294](https://github.com/Requarks/wiki/issues/2294))
- **Fixed:** Added logout endpoint for OAuth2 / OpenIDConnect module. ([#2395](https://github.com/Requarks/wiki/issues/849))
- **Fixed:** 2FA QR code now handles site names with invalid characters. ([#2397](https://github.com/Requarks/wiki/issues/849))
- **Fixed:** Force lowercase for email address on local auth. ([#2400](https://github.com/Requarks/wiki/issues/2400))
- **Fixed:** Permission validation no longer incorrectly fail for checks without page info. ([#2407](https://github.com/Requarks/wiki/issues/2407))

### Hotfix 1 *(2.5.126)*{.caption}
- **Fixed:** LDAP user avatar binary is now processed correctly. ([#849](https://github.com/Requarks/wiki/issues/849))
- **Fixed:** Login page is no longer empty on new installations. ([#2375](https://github.com/Requarks/wiki/issues/2375))
- **Fixed:** LDAP authentication is now passing strategy ID correctly. ([#2378](https://github.com/Requarks/wiki/issues/2378))
- **Fixed:** Discord auth is now using the updated endpoint URL. ([#2390](https://github.com/Requarks/wiki/issues/2390))

### Major Features *(2.5.117)*{.caption}

- New Login Experience
	- Add multiple instances of the same authentication strategy
	- Change the display order of instances
  - Rename the instances
  - Bypass Login Screen
  - Customize Login Background
  - Hide Local Provider
  - Reset Password
- OpenID Connect Authentication Module ([#2282](https://github.com/Requarks/wiki/issues/2282))
- 2FA (Two-Factor Authentication)
- Per-Group Redirection on Successful Login
- Per-Page JS Scripts + CSS Styles
- Page Publishing State (start/end date, private)
- Draw&#46;io Diagrams Integration for Markdown Editor

### Minor Improvements *(2.5.117)*{.caption}

- Image prefetching module for Kroki / PlantUML svg images.
- Optional underline parsing for Markdown using `_foo_` syntax.
- Improved Visual Editor Capabilities
	- Inline Code / Code Blocks
  - Table / Cell Properties
  - Sub / Superscript
  - Horizontal Line
  - Spellcheck
- Improved tables styling / match visual editor UI
- Experimental spellcheck mode for Markdown editor
- Improved Print View (with hidden comments)
- Improved display for Tabsets in Markdown Editor preview
- Added MultiMarkdown Tables capabilities to Markdown Editor
- Code Folding for Markdown Editor
- Purge History Utility

### Bug Fixes *(2.5.117)*{.caption}

- **Fixed:** Sideloaded locales are now processed before server starts. ([#1248](https://github.com/Requarks/wiki/issues/1248))
- **Fixed:** Include the locale code in sidebar browse links. ([#1807](https://github.com/Requarks/wiki/issues/1807))
- **Fixed:** Logout can now trigger Keycloak logout endpoint. ([#1934](https://github.com/Requarks/wiki/issues/1934))
- **Fixed:** Some links were not reconnected correctly during page move. ([#1991](https://github.com/Requarks/wiki/issues/1991))
- **Fixed:** Unauthorized admin access now returns status code 403 instead of 200. ([#2041](https://github.com/Requarks/wiki/issues/2041))
- **Fixed:** Use config value for tokenRenewal expiration. ([#2042](https://github.com/Requarks/wiki/issues/2042))
- **Fixed:** Editing buttons are no longer shown for pages the user doesn't have access to. ([#2043](https://github.com/Requarks/wiki/issues/2043))
- **Fixed:** Use first email address when retrieving multiple from LDAP. ([#2051](https://github.com/Requarks/wiki/issues/2051))
- **Fixed:** Tags are now filtered by access. ([#2100](https://github.com/Requarks/wiki/issues/2100))
- **Fixed:** Visualize Pages no longer return an SQL error for MySQL / MariaDB / SQLite installations. ([#2104](https://github.com/Requarks/wiki/issues/2104))
- **Fixed:** Deactivated users can no longer renew active tokens. ([#2105](https://github.com/Requarks/wiki/issues/2105))
- **Fixed:** Discord module was updated to use new endpoint URL. ([#2117](https://github.com/Requarks/wiki/issues/2117))
- **Fixed:** User is now added correctly via git when deleting a page. ([#2132](https://github.com/Requarks/wiki/issues/2132))
- **Fixed:** Navigation resolver is no longer public. ([#2178](https://github.com/Requarks/wiki/issues/2178))
- **Fixed:** Locale is now set correctly on edit, history and source pages. ([#2194](https://github.com/Requarks/wiki/issues/2194))
- **Fixed:** Pages with comments can now be deleted successfully. ([#2199](https://github.com/Requarks/wiki/issues/2199))
- **Fixed:** Search results can now scroll on overflow. ([#2232](https://github.com/Requarks/wiki/issues/2232))
- **Fixed:** Tags can now be fetched in the page GraphQL resolver. ([#2247](https://github.com/Requarks/wiki/issues/2247))
- **Fixed:** DB Password is now injected with surrounding quotes in docker config. ([#2293](https://github.com/Requarks/wiki/issues/2293))
- **Fixed:** Site title is now stripped of illegal characters upon saving. ([#2315](https://github.com/Requarks/wiki/issues/2315))
- **Fixed:** Prevent chrome from autofilling username in searchbar. ([#2324](https://github.com/Requarks/wiki/issues/2324))
- **Fixed:** Error UserDeleteForeignConstraint is now reporting the correct type. ([#2331](https://github.com/Requarks/wiki/issues/2331))
- **Fixed:** Creation date is now included in content dump metadata. ([#2345](https://github.com/Requarks/wiki/issues/2345))
- **Fixed:** Elasticsearch APM RUM client script now loads correctly. ([#2352](https://github.com/Requarks/wiki/issues/2352))
- **Fixed:** Any user / group modification now forces tokens to be revalidated on the next request.
- **Fixed:** A server restart / new instance forces tokens to be revalidated if issued before server start.
- **Fixed:** Matomo module siteId is now set correctly for users with javascript disabled.

# Previous Releases

- [2.0 to 2.4 Releases](/releases/previous)
- [2.0 Beta Releases](/releases/beta)