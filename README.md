# OutSystems Developer Workshops

A Hugo-based documentation site for OutSystems developer workshops built with Bootstrap, dark mode support, and responsive design.

## Quick Start

### Requirements
- Hugo 0.87.0 or later

### Commands

```bash
# Run locally
hugo server

# Build for production
hugo
```

The site will be available at `http://localhost:1313`

## Project Structure

```
├── content/                          # Workshop content
├── themes/outsystems-developer/      # Custom theme
│   ├── layouts/                     # HTML templates
│   ├── assets/css/style.css         # Styles + Bootstrap overrides
│   └── theme.toml
├── static/                          # Images and assets
├── hugo.toml                        # Site config
├── STYLE_GUIDE.md                   # Design guidelines
├── ACCESSIBILITY.md                 # A11y standards
└── spec-first-tdd/                  # TDD workflow
```

## Adding Workshops

1. Create `content/workshops/my-workshop/_index.md`
2. Add YAML frontmatter:

```yaml
---
title: "My Workshop"
description: "Description"
created: "2026-08-20"
authors:
  - name: "Author Name"
    role: "Role"
    company: "Company"
    image: "URL"
    link: "URL"
layout: single
---
```

3. Write content below frontmatter

## Theme Details

- **Framework**: Bootstrap 5.3.8 (via CDN)
- **Font**: DM Sans (Google Fonts)
- **Primary Color**: #ff4500 (Orange)
- **Dark Mode**: CSS variables + localStorage toggle
- **Layout**: 3-column (desktop) → responsive down to mobile

## Customization

- **Styles**: `themes/outsystems-developer/assets/css/style.css`
- **Layouts**: `themes/outsystems-developer/layouts/`
- **Config**: `hugo.toml`

See `STYLE_GUIDE.md` for design system details.

## Standards

- WCAG AA accessibility compliance
- Semantic HTML
- Mobile-first responsive design
- Light/dark mode support
