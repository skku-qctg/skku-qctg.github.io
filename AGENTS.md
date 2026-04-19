# AGENTS.md

This file provides guidance to coding agents working in this repository.

## Project Overview

This is the **SKKU Quantum Computing Theory Group** website, built on the [al-folio](https://github.com/alshedivat/al-folio) Jekyll theme. It is a static academic website hosted on GitHub Pages.

### Related Repository

- **Personal website**: `../seokhyung-lee.github.io` - Also an al-folio-based Jekyll site. It may share content such as publications or styling patterns with this group website.

## Common Commands

### Local Development with Docker (Recommended)

```bash
# Start the local development server (pulls the image and runs at http://localhost:8080)
docker compose pull
docker compose up

# Or use the slim image (< 100MB)
docker compose -f docker-compose-slim.yml up

# Rebuild the image after changes to Gemfile
docker compose up --build
```

**Port configuration**: Use port `8080` by default. If port `8080` is already occupied, use another available port such as `8081` or `8082`.

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
python bin/update_scholar_citations.py
```

**Google Scholar citations:**
- The script fetches citation counts using the `scholar_userid` from `_data/socials.yml`.
- Citation data is stored in `_data/citations.yml` with keys in the format `{scholar_userid}:{google_scholar_id}`.
- Each paper in `_bibliography/papers.bib` needs a `google_scholar_id` field to display citations.
- Citations are displayed as badges on the publications page via `_layouts/bib.liquid`.

## Architecture

### Content Structure

- `_pages/`: Static pages such as about, publications, and CV
- `_posts/`: Blog posts using the `YYYY-MM-DD-title.md` naming convention
- `_projects/`: Project showcase items
- `_news/`: News announcements shown on the about page
- `_bibliography/papers.bib`: Publications in BibTeX format
- `_teachings/`: Course pages with schedule support
- `_books/`: Bookshelf collection

### Configuration

- `_config.yml`: Main site configuration including URL, collections, plugins, and scholar settings
- `_data/cv.yml`: CV data in RenderCV format, used when `assets/json/resume.json` is absent
- `_data/socials.yml`: Social media links
- `_data/coauthors.yml`: Co-author links for publications; group members should set `group_member: true` for underline styling
- `_data/citations.yml`: Google Scholar citation counts, updated via `bin/update_scholar_citations.py`
- `_data/repositories.yml`: GitHub repositories to display
- `_data/members.yml`: Group member data including name, section, image, links, and optional bio content file

### Styling

- `_sass/`: SCSS files organized by feature
- `_sass/_themes.scss`: Theme colors including `--global-theme-color`
- `_sass/_variables.scss`: Global variables
- `_sass/_typography.scss`: Fonts and text styles
- `_sass/_components.scss`: Cards, profiles, and projects

### Layouts and Includes

- `_layouts/`: Page templates such as `page`, `post`, `bib`, and `course`
- `_includes/`: Reusable Liquid components

### Build System

- Jekyll builds static HTML into `_site/`.
- GitHub Actions in `.github/workflows/deploy.yml` automatically deploy to the `gh-pages` branch on pushes to `main`.
- ImageMagick generates responsive WebP images.

## Key Plugins

- `jekyll-scholar`: Bibliography management from BibTeX
- `jekyll-paginate-v2`: Pagination for posts and archives
- `jekyll-archives-v2`: Category and tag archive pages
- `jekyll-toc`: Automatic table of contents generation
- `jekyll-jupyter-notebook`: Jupyter notebook integration

## Publications

Edit `_bibliography/papers.bib` to add publications. Supported BibTeX fields include:

- `abstract`
- `arxiv`
- `pdf`
- `code`
- `slides`
- `poster`
- `video`
- `website`
- `blog`
- `preview` for thumbnails in `assets/img/publication_preview/`
- `bibtex_show` to show the BibTeX button

Author highlighting is configured in `_config.yml` under `scholar:`:

```yaml
scholar:
  last_name: [Lee]
  first_name: [Seok-Hyung, S.-H.]
```

## Creating Content

### New Blog Post

Create `_posts/YYYY-MM-DD-title.md` with front matter such as:

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

Create `_projects/name.md` with front matter including `title`, `description`, `img`, `importance`, and `category`.

### New News Item

Create `_news/announcement_N.md` with `layout: post`, `date`, and optional `inline: true` for inline display.

### New Group Member

Add an entry to `_data/members.yml`:

```yaml
- name: Full Name
  section: Group Leader | PhD Students | Master Students | Undergraduate Students | Alumni
  image: filename.jpg
  image_circular: true
  align: left
  content: about_name.md
  links:
    - type: website
      url: https://...
    - type: google_scholar
      url: https://scholar.google.com/citations?user=...
    - type: github
      url: https://github.com/...
    - type: email
      url: mailto:...
```

Place the image file in `assets/img/`. The `content` field is optional and should point to a bio file in `_pages/`.

Supported link types are `website`, `google_scholar`, `github`, `email`, `orcid`, and `linkedin`.
