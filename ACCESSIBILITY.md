# Accessibility Guidelines

This document outlines the accessibility standards for the OutSystems Developer Workshops site. All developers must follow these guidelines when creating or modifying content and components.

---

## 1. Semantic HTML Over Generic Divs

Use explicit semantic landmarks to structure your HTML meaningfully.

### Required Semantic Tags

- `<header>` — Site header and navigation area
- `<nav>` — Navigation menus and links
- `<main>` — Primary content area
- `<section>` — Major content divisions
- `<article>` — Self-contained content pieces
- `<footer>` — Site footer

### Interactive Elements

- **Always use `<button>` for actions** — clicking triggers an action, not navigation
- **Always use `<a>` for navigation** — clicking takes the user to a different page or location
- **Never put `onClick` handlers on `<div>` or `<span>` elements**

### Heading Hierarchy

- Maintain a logical heading hierarchy: `<h1>` → `<h2>` → `<h3>` → `<h4>` → `<h5>` → `<h6>`
- Never skip heading levels (e.g., jumping from `<h2>` to `<h4>`)
- Use only ONE `<h1>` per page

**Example:**
```html
<main>
  <article>
    <h1>Workshop Title</h1>
    <section>
      <h2>Module 1: Basics</h2>
      <h3>Introduction</h3>
    </section>
  </article>
</main>
```

---

## 2. Images & Multimedia

Every image must include an `alt` attribute that describes its content or purpose.

### Alt Text Guidelines

**Meaningful images:** Write concise, descriptive alt text
```html
<img src="/logo.svg" alt="OutSystems orange logo" />
<img src="/workshop.png" alt="BDD workshop participants" />
```

**Decorative images:** Use empty alt string
```html
<img src="/decoration.svg" alt="" />
```

**Complex images:** Provide context
```html
<img src="/architecture-diagram.svg" alt="Microservices architecture with API gateway, user service, and product service" />
```

---

## 3. Color & Contrast Compliance

All text must meet WCAG AA contrast ratio standards.

### Minimum Contrast Ratios

- **Standard text:** 4.5:1 ratio
- **Large text (18pt+):** 3:1 ratio

### Current Color Palette Compliance

| Color | Usage | Light Mode | Dark Mode | Contrast |
|-------|-------|-----------|-----------|----------|
| Black | Text | #000000 | - | ✅ 21:1 |
| White | Text | - | #ffffff | ✅ 21:1 |
| Orange | Accent | #ff4500 | #ff4500 | ✅ 4.6:1 |

### Color + Indicator Rule

Never use color alone to convey meaning:
- ❌ Don't: "Required fields are red"
- ✅ Do: "Required fields are marked with a red asterisk (*) and labeled 'Required'"

- ❌ Don't: "Click the green button to submit"
- ✅ Do: "Click the green Submit button"

---

## 4. Form Design

All form fields must be properly labeled and accessible.

### Label Requirements

Every form field must have an associated `<label>`:

```html
<!-- ✅ Correct -->
<label for="email">Email Address</label>
<input id="email" type="email" required />

<!-- ❌ Wrong -->
<input type="email" placeholder="Email" />
```

### Validation Messages

Provide explicit inline error messages:

```html
<label for="password">Password</label>
<input id="password" type="password" required aria-describedby="pwd-error" />
<span id="pwd-error" role="alert">Password must be at least 8 characters</span>
```

Never rely on color alone for validation states.

---

## 5. Keyboard Navigation & Focus Management

All interactive elements must be keyboard accessible.

### Focusable Elements

All interactive elements must be reachable via keyboard:
- Links (`<a>`)
- Buttons (`<button>`)
- Form inputs (`<input>`, `<select>`, `<textarea>`)
- Custom interactive components

### Focus Indicators

- ✅ Keep default browser focus indicators (blue outline)
- ✅ If replacing them, ensure they're **highly visible** (min 3px, high contrast)
- ❌ Never suppress focus with `outline: none` without a replacement

**Example of custom focus:**
```css
button:focus {
  outline: 3px solid #ff4500;
  outline-offset: 2px;
}
```

### Tab Order

- Use natural DOM order (correct HTML order = correct tab order)
- Never use `tabindex` unless absolutely necessary
- If you use `tabindex`, avoid values > 0 (they break natural ordering)

### Modals & Overlays

When using modals or dropdowns:
- Use `aria-expanded="true/false"` to indicate open/closed state
- Trap keyboard focus within the overlay
- Close modal with `Escape` key
- Return focus to the trigger element when modal closes

---

## Testing Checklist

Before shipping, verify:

- [ ] Semantic HTML tags used correctly
- [ ] All images have `alt` attributes
- [ ] All form fields have `<label>` elements
- [ ] Text contrast meets 4.5:1 minimum
- [ ] All interactive elements are keyboard accessible
- [ ] Focus indicators are visible
- [ ] Color is never the only indicator of state
- [ ] Heading hierarchy is logical (no skipped levels)
- [ ] Error messages are explicit text, not color-only

---

## Resources

- [WCAG 2.1 Guidelines](https://www.w3.org/WAI/WCAG21/quickref/)
- [MDN: HTML: A Good Basis for Accessibility](https://developer.mozilla.org/en-US/docs/Learn/Accessibility/HTML)
- [WebAIM: Contrast Checker](https://webaim.org/resources/contrastchecker/)
- [Accessible Foundations](https://www.a11y-101.com/)

---

## Questions?

If you have questions about accessibility guidelines, reach out to the team or consult the resources above. Accessibility is not optional — it's essential for an inclusive product.
