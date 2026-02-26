# John G. Turner - Author Website

## Project Overview

This is the personal website for John G. Turner, a historian of American religion and professor at George Mason University. The site showcases his published books, scholarship projects, and media appearances. It is built with Hugo and hosted at johngturner.com.

## Technology

- **Static site generator**: Hugo (requires extended edition for image processing)
- **CSS framework**: Bootstrap 5.3.3 via CDN (CSS only, no JS)
- **Font**: Gelasio (Google Fonts)
- **Custom styles**: `static/css/custom.css`

## Content Types

### Book (`content/book/*/index.md`)
Page bundles with a `cover.*` image. Front matter: title, tagline, weight, publisher, year, isbn, pull_quotes (array), purchase_links (array). Displayed on the homepage via the `book-card.html` partial. Weight controls display order (1 = first).

### Scholarship (`content/scholarship/*/index.md`)
Page bundles with an optional `thumbnail.*` image. Front matter: title, link, weight. Displayed on the homepage below books.

### Media (`content/media/*.md`)
Plain markdown files (no page bundles). Front matter: title, source, link, youtube_id (optional), topic, weight. Displayed on the media page grouped by topic. If `youtube_id` is set, the item renders as an embedded YouTube video.

### Pages
Standard markdown files like `content/about.md`.

## Image Processing

Images in page bundles are processed via `layouts/partials/processed-image.html`, which generates 1x and 2x retina versions using Hugo's image pipeline. The `layouts/shortcodes/img.html` shortcode provides the same capability in markdown body content:

```
{{</* img src="cover.jpg" alt="Book cover" width="400" */>}}
```

## Site Structure

- **Home** (`/`): Intro text, all books sorted by weight, scholarship projects
- **About** (`/about/`): Biographical narrative
- **Media** (`/media/`): Media appearances grouped by topic with YouTube embeds

Navigation menu is defined in `hugo.yaml` under `menus.main`.

## Key Directories

- `content/` -- All site content as markdown with YAML front matter
- `layouts/` -- Hugo templates, partials, and shortcodes
- `static/css/` -- Custom CSS
- `archetypes/` -- Templates for creating new content
- `zzz-old-website/` -- The previous hand-coded site (kept for reference)

## Development

```
hugo server -D
```

## Adding Content

To add a new book:
1. Create `content/book/book-slug/index.md` with book front matter
2. Add `cover.jpg` (or `.png`, `.webp`) to the same directory
3. Set `weight` to control position on homepage

To add a media item:
1. Create `content/media/item-slug.md` with media front matter
2. Set `topic` to match an existing topic group heading
3. Set `youtube_id` if it's a YouTube video to enable embedding

Topic display order on the media page is controlled by the hardcoded slice in `layouts/media/list.html`.
