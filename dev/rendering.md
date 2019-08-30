---
title: Rendering
description: Developing Rendering Modules
published: true
date: 2019-05-24T19:34:43.159Z
tags: 
---

A rendering module adds extra content processing features to the wiki. It's part of the rendering pipeline in which raw content gets parsed and transformed into a final HTML form.

# Architecture

## Creating a New Page

![Create Page Flow Diagram](/assets/diagrams/diag-create-page-flow.jpg =1000x){.decor-shadow .radius-4}

## View a Page

![View Page Flow Diagram](/assets/diagrams/diag-view-page-flow.jpg =1000x){.decor-shadow .radius-4}

# Rendering Modules

There are 2 types of rendering modules: **Core Rendering Modules** and **Extension Rendering Module**.

## Core Rendering Module

A core rendering module \(CRM\) takes a specific format as input \(e.g. Markdown\), optionally uses one or many extension rendering modules \(ERM\) and outputs the result into another format \(usually HTML\).

There's usually 1 CRM per input format type, but multiple can be executed serially. However, note that order cannot be guaranteed between CRMs of the same input type.

It's the job of the CRM to load ERM to be applied and execute them in order as part of the rendering process.

## Extension Rendering Module

Extension rendering modules \(ERM\) are consumed by core rendering modules \(CRM\). They cannot run by themselves and usually process a very specific part of a core module.

For example, an ERM for a Markdown CRM could be to transform emoji tags into symbols. It's a specific feature that relies on the Markdown CRM engine.

![Rendering Pipeline Diagram](/assets/diagrams/diag-rendering-pipeline.jpg =1000x){.decor-shadow .radius-4}
