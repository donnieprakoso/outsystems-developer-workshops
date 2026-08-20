# OutSystems Developer Workshops (Hugo) — Style Guide

**This is the source of truth for all design decisions. Every developer must follow these guidelines without exception.**

---

## Technology Stack

- **Static Site Generator**: Hugo
- **Theme**: outsystems-developer (located in `themes/outsystems-developer/`)
- **Config File**: `hugo.toml`
- **Content Format**: Markdown (TOML frontmatter)
- **CSS**: `themes/outsystems-developer/assets/css/style.css`

---

## Color Palette

### Light Mode (Default)
- **Background**: `#ffffff` (white)
- **Text**: `#000000` (black)
- **Links**: `#000000` (black)
- **Accent/Orange**: `#ff4500` (OutSystems orange — for focus outlines)

### Dark Mode
- **Background**: `#000000` (pure black)
- **Text**: `#ffffff` (white)
- **Links**: `#ffffff` (white)
- **Accent/Orange**: `#ff4500` (OutSystems orange — for focus outlines)

**Rule**: Dark mode is the exact inversion of light mode. If a color works in light mode, apply its inverse in dark mode.

---

## Adding Workshop Content

All workshop content lives in `content/workshops/`.

### Frontmatter Format

```toml
+++
title = "Workshop Title"
description = "Short description"
created = "2026-08-20"
updated = "2026-08-20"
authors = [
  {name = "Author Name", role = "Role", company = "Company", image = "URL", link = "URL"}
]
+++
```

**Fields:**
- `title` — Page title (required)
- `description` — Short description for listing
- `created` — ISO date (YYYY-MM-DD)
- `updated` — ISO date (YYYY-MM-DD)
- `authors` — Array of author objects with name, role, company, image URL, and link

### Creating a New Workshop

1. Create file in `content/workshops/your-workshop.md`
2. Add TOML frontmatter with required fields
3. Write content in Markdown
4. Hugo automatically generates the page

---

## Typography

### Heading Sizes

| Heading | Size | Usage |
|---------|------|-------|
| H1 | 2.5rem | Page title |
| H2 | 1.5rem | Major sections |
| H3 | 1.2rem | Subsections |
| H4 | 1.1rem | Minor subsections |

### Best Practices

- Use H1 only once per page (the page title)
- Never skip heading levels
- Keep hierarchy logical and semantic

---

## Links

### Link Styles

| State | Light Mode | Dark Mode | Style |
|-------|-----------|-----------|-------|
| Normal | Black | White | No underline |
| Hover | Black | White | Underline |
| Focus | Black + orange outline | White + orange outline | Outline |

**CSS Implementation** (in `assets/css/style.css`):
```css
a { color: var(--link-color); text-decoration: none; }
a:hover { text-decoration: underline; }
a:focus { outline: 2px solid var(--color-primary); outline-offset: 2px; }
```

---

## Buttons

### Light Mode
- **Background**: Transparent
- **Border**: 2px orange
- **Text**: Black

### Dark Mode
- **Background**: Orange
- **Border**: None
- **Text**: White

---

## Layouts & Templates

### Available Layouts

- **single.html** — Individual workshop pages
- **list.html** — Workshop listing pages
- **baseof.html** — Base template for all pages

### Layout Features

- **Author box** — Displays automatically if `authors` in frontmatter
- **Timestamps** — Shows created/updated dates if present
- **Navigation** — Previous/next workshop links

---

## Accessibility

Refer to `ACCESSIBILITY.md` for complete guidelines.

**Quick checklist:**
- ✅ Semantic HTML tags (`<header>`, `<nav>`, `<main>`, etc.)
- ✅ All images have `alt` text
- ✅ Links have visible focus states
- ✅ Color contrast meets WCAG AA (4.5:1 minimum)
- ✅ Keyboard navigation works throughout

---

## Creating New Layouts

1. Create file in `themes/outsystems-developer/layouts/_default/your-layout.html`
2. Use Hugo template syntax
3. Access page data: `{{ .Title }}`, `{{ .Content }}`, `{{ .Params }}`
4. Reference the theme CSS: `<link rel="stylesheet" href="{{ `css/style.css` | relURL }}">`

---

## CSS Customization

Edit `themes/outsystems-developer/assets/css/style.css` to:
- Update colors (modify CSS custom properties in `:root`)
- Adjust typography sizes
- Change spacing and layout
- Add responsive breakpoints

**Custom Properties:**
```css
:root {
  --color-primary: #ff4500;
  --color-bg-light: #ffffff;
  --color-text-light: #000000;
  --color-gray-1: #f5f5f5;
  /* ... more colors ... */
}
```

---

## Menu Navigation

Edit `hugo.toml` to modify menu items:

```toml
[[menu.main]]
  name = "Menu Item"
  url = "/path/"
  weight = 1
```

---

## References

- **Accessibility Standards**: See `ACCESSIBILITY.md`
- **Hugo Documentation**: https://gohugo.io/documentation/
- **Theme Config**: `themes/outsystems-developer/theme.toml`
- **Site Config**: `hugo.toml`
