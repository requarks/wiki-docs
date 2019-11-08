---
title: Introduction to Wiki.js
description: How to create your first page and more
published: true
date: 2019-11-08T19:24:26.023Z
tags: 
---

# The Interface

![Interface](/assets/ui/ui-basics.jpg){.decor-radius .decor-shadow}

### Global
- **Navigation Menu** - Menu to go Home, Browse the Wiki Structure or Browse by Tags.
- **Global Navigation** - A persistent navigation menu, displayed on all pages. Usually consists of important pages or links to external websites.
- **Global Search** - Quickly find a page by performing a search.
- **Create New Page** - Create a new page.
- **User Menu** - User-specific actions such as View Profile, Administration and Logout.
{.grid-list .body-2}

### Per Page
- **Page Actions** - List of actions on the current page, such as Edit, Move, Delete, History, etc.
- **Breadcrumbs** - Full Path to the current page. Represents the folder structure.
- **Table of Contents** - Sections of the current page. Based on the headers in the content.
- **Page Tags** - Tags associated to the current page. See related pages by clicking on a tag.
- **Author** - View the author and date of the last modification of the page.
- **Social Links** - Sharing / Printing Links for the current page.
- **Edit Page / Page Actions** - Quick access menu to edit or perform other actions on the current page.
{.grid-list .body-2}

# Basics

## Create New Page

In order to create a new page, click the **New Page** button, located in the top right corner of the page.

The following dialog will appear:
![New Page Dialog](/assets/ui/ui-newpage-dialog.png =600x){.decor-shadow .radius-5}

1. Select the language to create the page for *(the current locale is selected by default)*.
2. Enter the full path to the page you want to create.
	- The path should contain no spaces *(use dashes instead)* and consists of URL-safe characters.
  	- **DO NOT** put a trailing slash.
  	- You don't need to create folders. Enter the full path you want to create and folders will be created automatically. For example, enter `universe/planets/earth` to automatically create the universe and planets subfolders.
3. Click **Select** to proceed.