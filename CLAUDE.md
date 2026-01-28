# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is the **SKKU Quantum Computing Theory Group** website, built on the [al-folio](https://github.com/alshedivat/al-folio) Jekyll theme. It's a static academic website hosted on GitHub Pages.

## Common Commands

### Local Development with Docker (Recommended)

```bash
# Start local development server (pulls image and runs at http://localhost:8080)
docker compose pull
docker compose up

# Or use slim image (< 100MB)
docker compose -f docker-compose-slim.yml up

# Rebuild image after changes to Gemfile
docker compose up --build
```

### Local Development without Docker

```bash
# Install dependencies
bundle install
pip install jupyter

# Serve locally at http://localhost:4000
bundle exec jekyll serve

# Build for production
JEKYLL_ENV=production bundle exec jekyll build
```

### Code Formatting

```bash
# Format code with Prettier
npx prettier --write .
```

### Utility Scripts

```bash
# Update Google Scholar citations
python3 bin/update_scholar_citations.py
```

## Architecture

### Content Structure

- **`_pages/`**: Static pages (about, publications, cv, etc.)
- **`_posts/`**: Blog posts (format: `YYYY-MM-DD-title.md`)
- **`_projects/`**: Project showcase items
- **`_news/`**: News announcements for the about page
- **`_bibliography/papers.bib`**: Publications in BibTeX format
- **`_teachings/`**: Course pages with schedule support
- **`_books/`**: Bookshelf collection

### Configuration

- **`_config.yml`**: Main site configuration (URL, collections, plugins, scholar settings)
- **`_data/cv.yml`**: CV data in RenderCV format (fallback if `assets/json/resume.json` is absent)
- **`_data/socials.yml`**: Social media links
- **`_data/coauthors.yml`**: Co-author links for publications
- **`_data/repositories.yml`**: GitHub repos to display

### Styling

- **`_sass/`**: SCSS files organized by feature
  - `_themes.scss`: Theme colors (`--global-theme-color`)
  - `_variables.scss`: Global variables
  - `_typography.scss`: Fonts and text styles
  - `_components.scss`: Cards, profiles, projects

### Layouts & Includes

- **`_layouts/`**: Page templates (page, post, bib, course, etc.)
- **`_includes/`**: Reusable Liquid components

### Build System

- Jekyll builds static HTML to `_site/`
- GitHub Actions (`.github/workflows/deploy.yml`) auto-deploys to `gh-pages` branch on push to main
- ImageMagick generates responsive WebP images

## Key Plugins

- **jekyll-scholar**: Bibliography management from BibTeX
- **jekyll-paginate-v2**: Pagination for posts/archives
- **jekyll-archives-v2**: Category/tag archive pages
- **jekyll-toc**: Auto table of contents
- **jekyll-jupyter-notebook**: Jupyter notebook integration

## Publications

Edit `_bibliography/papers.bib` to add publications. Supported BibTeX fields:
- `abstract`, `arxiv`, `pdf`, `code`, `slides`, `poster`, `video`, `website`, `blog`
- `preview` (thumbnail image in `assets/img/publication_preview/`)
- `bibtex_show` (shows BibTeX button)

Author highlighting configured in `_config.yml` under `scholar:`:
```yaml
scholar:
  last_name: [Lee]
  first_name: [Seok-Hyung, S.-H.]
```

## Creating Content

### New Blog Post
Create `_posts/YYYY-MM-DD-title.md` with frontmatter:
```yaml
---
layout: post
title: Your Title
date: YYYY-MM-DD HH:MM:SS
description: Brief description
tags: [tag1, tag2]
categories: [category]
---
```

### New Project
Create `_projects/name.md` with frontmatter including `title`, `description`, `img`, `importance`, `category`.

### New News Item
Create `_news/announcement_N.md` with `layout: post`, `date`, and optional `inline: true` for inline display.
