# File-Based Content

Store posts, pages, and custom post types as Markdown files.

## Overview

PraisonPressGit enables a file-based content management approach where your WordPress content lives in Markdown files, not just the database.

## Content Format

Create `.md` files with YAML front matter:

```markdown
---
title: "My Post Title"
slug: "my-post-slug"
author: "admin"
date: "2024-10-31 12:00:00"
status: "publish"
categories:
  - "General"
tags:
  - "example"
---

# Your content here

Write your content in Markdown format.
```

## Directory Structure

```
/content/
├── posts/              # Blog posts
├── pages/              # Static pages
├── recipes/            # Custom post type: Recipes
└── config/             # Configuration files
```

## Automatic Post Type Discovery

Simply create a new directory to add a custom post type:

```bash
mkdir /content/recipes
```

The plugin will automatically:
- Register the `recipes` post type
- Create the URL route `/recipes/{slug}`
- Load content from the directory

## Front Matter Fields

| Field | Required | Description |
|-------|----------|-------------|
| `title` | ✅ | Post title |
| `slug` | ✅ | URL slug |
| `date` | ✅ | Publication date |
| `status` | ❌ | Post status (default: publish) |
| `author` | ❌ | Author username |
| `categories` | ❌ | Category list |
| `tags` | ❌ | Tag list |
| `featured_image` | ❌ | Featured image URL |

## Benefits

| Benefit | Description |
|---------|-------------|
| 🔄 Version Control | Track changes with Git |
| 📁 Portable | Content moves with your files |
| ⚡ Fast | No database queries |
| 👥 Collaborative | PR-based workflows |
