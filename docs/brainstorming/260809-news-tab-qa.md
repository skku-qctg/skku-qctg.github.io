# News Tab Brainstorming Q&A

## Original Request

Create a dedicated tab that collects announcements on the SKKU QCTG website. Investigate whether the existing al-folio theme already provides a similar feature before designing a custom implementation.

## Repository Findings

- The repository already has al-folio's `news` collection configured in `_config.yml`.
- `_pages/news.md` already exposes a complete news index at `/news/`.
- `_includes/news.liquid` supports both inline items and title-linked detail pages.
- The News page is currently omitted from the navbar because it has no navigation metadata.
- The `_news/` collection currently contains no entries.
- The optional homepage news preview is currently disabled.

## Decisions

### Q1

Which public-facing structure should be used: a Notice tab at `/notice/`, a Notice tab at `/news/`, or a separate `_notices` collection?

### A1

Reuse the existing al-folio News page and collection at `/news/`; do not introduce a new collection or a `/notice/` route.

### Q2

How should individual announcements appear: mixed inline and linked items, inline only, or detail pages only?

### A2

Use the mixed format. Short announcements may appear inline, while longer announcements may use a title-linked detail page. The navbar label should be `News`, not `Notice`.

### Q3

Should the homepage also show a small News preview, or should News appear only as a dedicated tab?

### A3

Use the dedicated News tab only. Keep the existing homepage preview disabled.

### Q4

Where should the News tab appear in the navbar?

### A4

Place News after Group Members. The intended ordering is `Publications → Group Members → News`.

### Q5

Which implementation approach should be used: native al-folio activation only, native activation plus authoring documentation, or a customized News interface?

### A5

Use native al-folio activation only. Add the navigation metadata needed to expose the existing News page while preserving the current `/news/` route, mixed-format rendering, and disabled homepage preview. Do not add authoring documentation or custom News features in this iteration.

### Q6

Should the confirmed design proceed through a saved specification, an automatically reviewed specification, full-auto delivery, or direct implementation?

### A6

Proceed directly to implementation without creating a separate specification.

## Post-Implementation Revision

After reviewing the first published item locally, the user changed the public section name from `News` to `Notice`, changed the index URL from `/news/` to `/notice/`, and requested category tabs ordered as `All`, `Hiring`, and `News`. The first postdoctoral recruitment item belongs to `Hiring`. The internal al-folio collection remains `_news` for compatibility.
