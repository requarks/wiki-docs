---
title: Folder Structure & Tags
description: Learn how to categorize your pages for easier navigation.
published: true
date: 2022-05-26T07:30:51.103Z
tags: user-guide
editor: markdown
dateCreated: 2019-11-10T18:15:56.841Z
---

# Folder Structure

Wiki.js doesn't have a folder structure in the traditional sense. You never need to create folders in order to create new pages. Instead, you create pages directly at the path of your choice.

For example, in order to create a page at `/universe/planets/earth`, you don't need to create the folders `universe` and `planets` in the first place. They'll be inferred automatically.

![Folder Structure](/assets/diagrams/diag-folder-structure.jpg =650x){.decor-shadow .radius-5}

This system allows for greater flexibility and less dependencies between pages. However that doesn't mean you can't use a traditional folder system should you want to. The folder structure is still available when creating and moving pages. The only difference being you don't have to manage folders, they are inferred automatically from pages paths.

## Breadcrumbs

The breadcrumbs bar shown on top of every page is generated automatically from the path.

## Nesting

When creating multi-level pages, you may want to have a landing page for each of the virtual folders.

For example, if you have a page at path `/foo/bar`, you should create a new page at path `/foo`. This will ensure that clicking the "**foo**" breadcrumbs link on the `/foo/bar` page leads to the `/foo` page.

If you're using the **Site Tree** navigation mode (or **Custom Navigation**), the page title for each level is taken from its corresponding page.

### Nesting Example

For example, by creating the following pages:

- Page at path `/universe` with title "*The Universe*"
- Page at path `/universe/planets` with title "*The Planets*"
- Page at path `/universe/planets/earth` with title "*The Blue Marble*"

would create a site tree with the following entries:
- **The Universe**
	- **The Planets**
  		- **The Blue Marble**
      
On "*The Blue Marble*" page, you would have a breadcrumb similar to:

*:*{.mdi .mdi-home} / **universe** / **planets** / **earth**

with each link corresponding to the 3 pages created above.

# Tags

Tags are a great way to categorize your pages and easily find related content. They are a much leaner alternative to using a complex system of folders to categorize your content. Tags are simple labels attached to a page.

## Set Tags

Multiple tags can be added to a page.

For example, for a page about the city **Montreal**, you could add tags `cities`, `canada`, `north-america`. These tags can then be used to quickly find the page afterwards. By browsing by tags `canada` and `cities`, the page **Montreal** will come up in the results because both of these tags are present on the page.

More tags can be added or removed from a page at any time.

## Browse Tags

Use the **Browse by Tags** link (located next to the search bar, or in the navigation menu) to see a list of all tags available in the wiki.

Select one or multiple tags to view a list of pages matching the selection.