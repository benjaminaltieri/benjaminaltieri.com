# CLAUDE.md — AI Assistant Guide for benjaminaltieri.com

## Project Overview

Personal blog and portfolio site for Ben Altieri, built with **Zola** (a Rust-based static site generator). The site uses a terminal-aesthetic dark theme called **zerm** with a red/coral accent color.

**Live site**: benjaminaltieri.com
**Hosting**: Vercel (deployed via Git integration)
**Main branch**: `master`

## Tech Stack

- **Static site generator**: [Zola](https://www.getzola.org/) (v0.20.0+)
- **Theme**: [zerm](https://github.com/ejmg/zerm) — installed as a Git submodule at `themes/zerm/`
- **Styling**: Theme Sass + custom CSS overrides in `static/custom.css`
- **Fonts**: Inter (body), JetBrains Mono (headings/nav), Fira Code (code blocks)
- **Math**: KaTeX enabled for pages with `math=true` in front matter
- **Feeds**: Atom feed at `atom.xml`

## Repository Structure

```
benjaminaltieri.com/
├── config.toml              # Zola site configuration (theme, taxonomies, menus, extras)
├── content/
│   ├── _index.md            # Home page (root section)
│   ├── a_post.md            # Draft placeholder blog post
│   └── about/
│       └── _index.md        # About Me page at /about/
├── static/
│   └── custom.css           # Custom CSS overrides for the zerm theme
├── templates/
│   ├── index.html           # Custom home/section template (overrides theme default)
│   └── macros/
│       ├── footer.html      # Copyright and script macros
│       └── head.html        # Font loading, styling, favicon, RSS, meta, KaTeX macros
├── themes/
│   └── zerm/                # Git submodule (must be initialized before building)
├── .gitmodules              # Submodule configuration for zerm theme
└── CLAUDE.md                # This file
```

## Build & Development Commands

```bash
# Initialize theme submodule (required before first build)
git submodule update --init

# Local development server with live reload
zola serve

# Production build (outputs to public/)
zola build

# Check for broken links and other issues
zola check
```

There is no `Makefile`, `package.json`, CI config, or `vercel.json`. Vercel auto-detects Zola and handles builds on deploy.

## Content Authoring

### Adding a New Blog Post

Create a Markdown file in `content/` with Zola front matter:

```markdown
+++
title = "Post Title"
date = 2025-12-01
description = "Brief description"
[taxonomies]
categories = ["category"]
tags = ["tag1", "tag2"]
+++

Post content here...
```

- Set `draft = true` in front matter to hide from the published site
- The home page paginates posts with `paginate_by = 5`
- Available taxonomies: `categories`, `tags`, `technologies`

### Adding a New Section

Create a directory under `content/` with an `_index.md` file:

```
content/new-section/_index.md
```

## Template Architecture

The site uses a **minimal override strategy** — only 3 custom template files exist, while the rest come from the zerm theme:

- **`templates/index.html`** — The main section/home template. Imports macros from both custom files and the theme. Renders home page intro text as an `<article>` when `section.content` exists, otherwise falls back to a post list.
- **`templates/macros/head.html`** — Custom `<head>` macros: `fonts()`, `styling()`, `favicon()`, `rss()`, `general_meta()`, `katex()`.
- **`templates/macros/footer.html`** — Custom footer macros: `copyright()` (defaults to "© YEAR Ben Altieri :: Built with Zola") and `script()`.

Theme macros imported but not overridden: `logo`, `header`, `lists`, `posts`, `social`, `utils`, `menu`, `pagination`, `extended_header`, `extended_footer`, `comments`.

## Styling Conventions

- **Do not fork or modify theme Sass directly.** Add CSS overrides in `static/custom.css` instead.
- The theme color is `red` (set in `config.toml` as `theme_color`). This maps to `themes/zerm/static/color/red.css` and exposes `var(--accent)` and `var(--accent-alpha-20)`.
- Custom CSS uses the theme's CSS variables (e.g., `var(--accent)`, `var(--accent-alpha-20)`).
- The About page contains an embedded HTML "Full System Stack" visualization styled via `.system-stack`, `.stack-layer`, `.stack-skill` classes in `custom.css`.
- Responsive breakpoint: 768px (grid collapses to single column).

## Configuration Reference (`config.toml`)

Key settings an AI assistant should be aware of:

| Setting | Value | Notes |
|---------|-------|-------|
| `base_url` | `/` | Relative for Vercel compatibility |
| `theme` | `zerm` | Do not change without updating templates |
| `theme_color` | `red` | Options: orange, blue, red, green, pink |
| `logo_text` | `:: SYSTEM_LOG` | Top-left branding text |
| `center` | `true` | Centered layout |
| `full_width` | `false` | Not full-width |
| `enable_katex` | `true` | Math rendering available |
| `compile_sass` | `true` | Theme Sass auto-compiled |
| `build_search_index` | `true` | Search index generated |

## Key Conventions

1. **Theme is a submodule** — never commit changes inside `themes/zerm/`. If theme customization is needed, override in `templates/` or `static/custom.css`.
2. **Minimal template overrides** — only override theme templates when necessary. Import and reuse theme macros wherever possible.
3. **CSS over Sass** — custom styles go in `static/custom.css`, not in a `sass/` directory, to keep overrides simple and separate from theme code.
4. **Content uses Zola conventions** — `_index.md` for sections, regular `.md` files for pages/posts, TOML front matter delimited by `+++`.
5. **Draft posts** — use `draft = true` in front matter. The existing `a_post.md` is a draft placeholder.
6. **Embedded HTML in content** — the About page uses raw HTML blocks within Markdown for the system stack visualization. This is a valid Zola pattern.
7. **External links in menu** — menu items with `external=true` open in new tabs.

## Common Tasks

### Changing the site branding
Edit `logo_text` in `config.toml`.

### Adding a menu item
Add to `main_menu` in `config.toml`. Use `external=true` for external links.

### Modifying the home page intro
Edit `content/_index.md`.

### Updating the About page
Edit `content/about/_index.md`. The system stack visualization is raw HTML within the Markdown file.

### Adding custom styles
Append to `static/custom.css`. Use theme CSS variables for consistency.

### Changing the accent color
Set `theme_color` in `config.toml` to one of: `orange`, `blue`, `red`, `green`, `pink`.
