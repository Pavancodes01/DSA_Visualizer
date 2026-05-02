---
name: html-css
description: >
  Use this skill whenever the user asks to build, style, or fix HTML/CSS files.
  Covers page layouts, components, responsive design, animations, dark mode,
  utility classes, and CSS best practices. Triggers include: "create a webpage",
  "style this component", "make it responsive", "fix my CSS", "add animations",
  "build a landing page", or any task producing .html / .css files.
---

## Overview

This skill guides creation of clean, responsive, and well-structured HTML and CSS.
The goal is production-quality code that is readable, maintainable, and works across devices.

---

## HTML Best Practices

### 1. Always Use Semantic Tags
Use the right HTML element for the right purpose. This helps browsers, screen readers, and search engines understand your page.

```html
<!-- BAD: div soup -->
<div class="header">
  <div class="nav">...</div>
</div>
<div class="main-content">...</div>
<div class="footer">...</div>

<!-- GOOD: semantic HTML -->
<header>
  <nav>...</nav>
</header>
<main>
  <article>...</article>
  <aside>...</aside>
</main>
<footer>...</footer>
```

**Key semantic tags to use:**
- `<header>`, `<footer>`, `<nav>`, `<main>`, `<aside>` — page structure
- `<section>` — a thematic group of content
- `<article>` — a standalone piece of content (blog post, card)
- `<figure>` + `<figcaption>` — images with captions
- `<button>` — clickable actions (NOT `<div onclick="">`)
- `<a>` — navigation/links (NOT `<div onclick="">`)

### 2. Always Include a Proper Boilerplate

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <meta name="description" content="Page description here" />
  <title>Page Title</title>
  <link rel="stylesheet" href="style.css" />
</head>
<body>
  <!-- content here -->
</body>
</html>
```

### 3. Accessibility (a11y) — Always Add These

```html
<!-- Images must have alt text -->
<img src="logo.png" alt="Company logo" />

<!-- Buttons must have clear labels -->
<button aria-label="Close menu">✕</button>

<!-- Forms must have labels linked to inputs -->
<label for="email">Email</label>
<input type="email" id="email" name="email" required />

<!-- Use role and aria where needed -->
<nav aria-label="Main navigation">...</nav>
```

---

## CSS Best Practices

### 1. Use CSS Custom Properties (Variables) for Theming

Define all colors, fonts, and spacing in one place at the top. This makes changing the theme easy.

```css
:root {
  /* Colors */
  --color-primary: #2563eb;
  --color-primary-hover: #1d4ed8;
  --color-bg: #ffffff;
  --color-text: #1f2937;
  --color-muted: #6b7280;
  --color-border: #e5e7eb;

  /* Typography */
  --font-sans: 'Inter', sans-serif;
  --font-size-sm: 0.875rem;
  --font-size-base: 1rem;
  --font-size-lg: 1.125rem;
  --font-size-xl: 1.25rem;
  --font-size-2xl: 1.5rem;

  /* Spacing */
  --space-1: 0.25rem;
  --space-2: 0.5rem;
  --space-4: 1rem;
  --space-6: 1.5rem;
  --space-8: 2rem;

  /* Borders */
  --radius-sm: 4px;
  --radius-md: 8px;
  --radius-lg: 16px;
  --radius-full: 9999px;

  /* Shadows */
  --shadow-sm: 0 1px 3px rgba(0,0,0,0.1);
  --shadow-md: 0 4px 12px rgba(0,0,0,0.1);
}
```

### 2. CSS Reset / Base Styles

Always include a base reset to remove browser inconsistencies.

```css
*, *::before, *::after {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

html {
  scroll-behavior: smooth;
}

body {
  font-family: var(--font-sans);
  font-size: var(--font-size-base);
  color: var(--color-text);
  background-color: var(--color-bg);
  line-height: 1.6;
  -webkit-font-smoothing: antialiased;
}

img, video {
  max-width: 100%;
  display: block;
}

a {
  color: inherit;
  text-decoration: none;
}

button {
  cursor: pointer;
  border: none;
  background: none;
  font: inherit;
}
```

### 3. Layout — Use Flexbox and Grid

**Flexbox** — for one-directional layouts (rows or columns):
```css
/* Centering something */
.center {
  display: flex;
  align-items: center;
  justify-content: center;
}

/* Navbar */
.navbar {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: var(--space-4);
}

/* Card row */
.card-row {
  display: flex;
  flex-wrap: wrap;
  gap: var(--space-4);
}
```

**Grid** — for two-directional layouts (rows AND columns):
```css
/* Auto-fill responsive grid */
.grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
  gap: var(--space-6);
}

/* Classic 2-column layout */
.two-col {
  display: grid;
  grid-template-columns: 1fr 2fr;
  gap: var(--space-8);
}
```

### 4. Responsive Design — Mobile First

Always write styles for **mobile first**, then add breakpoints for larger screens.

```css
/* Mobile first — default styles are for mobile */
.container {
  width: 100%;
  padding: 0 var(--space-4);
}

/* Tablet (768px and up) */
@media (min-width: 768px) {
  .container {
    max-width: 720px;
    margin: 0 auto;
  }
}

/* Desktop (1024px and up) */
@media (min-width: 1024px) {
  .container {
    max-width: 1100px;
  }
}
```

**Standard breakpoints to use:**
| Name     | Width        |
|----------|-------------|
| Mobile   | < 768px     |
| Tablet   | ≥ 768px     |
| Desktop  | ≥ 1024px    |
| Wide     | ≥ 1280px    |

### 5. Dark Mode Support

```css
:root {
  --color-bg: #ffffff;
  --color-text: #1f2937;
  --color-border: #e5e7eb;
}

@media (prefers-color-scheme: dark) {
  :root {
    --color-bg: #0f172a;
    --color-text: #f1f5f9;
    --color-border: #334155;
  }
}
```

Because you used CSS variables everywhere, dark mode works automatically — you only need to override the variables.

### 6. Animations & Transitions

Keep animations subtle and purposeful. Prefer CSS over JavaScript for simple effects.

```css
/* Smooth hover transitions */
.btn {
  background: var(--color-primary);
  color: white;
  padding: var(--space-2) var(--space-4);
  border-radius: var(--radius-md);
  transition: background 0.2s ease, transform 0.1s ease, box-shadow 0.2s ease;
}

.btn:hover {
  background: var(--color-primary-hover);
  transform: translateY(-1px);
  box-shadow: var(--shadow-md);
}

.btn:active {
  transform: translateY(0);
}

/* Fade-in animation */
@keyframes fadeIn {
  from { opacity: 0; transform: translateY(10px); }
  to   { opacity: 1; transform: translateY(0); }
}

.fade-in {
  animation: fadeIn 0.4s ease forwards;
}

/* Respect users who prefer no animations */
@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after {
    animation-duration: 0.01ms !important;
    transition-duration: 0.01ms !important;
  }
}
```

### 7. Common Reusable Components

**Button:**
```css
.btn {
  display: inline-flex;
  align-items: center;
  gap: var(--space-2);
  padding: var(--space-2) var(--space-6);
  font-size: var(--font-size-base);
  font-weight: 600;
  border-radius: var(--radius-md);
  transition: all 0.2s ease;
}

.btn-primary {
  background: var(--color-primary);
  color: #fff;
}

.btn-outline {
  background: transparent;
  border: 2px solid var(--color-primary);
  color: var(--color-primary);
}
```

**Card:**
```css
.card {
  background: var(--color-bg);
  border: 1px solid var(--color-border);
  border-radius: var(--radius-lg);
  padding: var(--space-6);
  box-shadow: var(--shadow-sm);
  transition: box-shadow 0.2s ease;
}

.card:hover {
  box-shadow: var(--shadow-md);
}
```

**Input:**
```css
.input {
  width: 100%;
  padding: var(--space-2) var(--space-4);
  font-size: var(--font-size-base);
  border: 1.5px solid var(--color-border);
  border-radius: var(--radius-md);
  background: var(--color-bg);
  color: var(--color-text);
  transition: border-color 0.2s ease;
  outline: none;
}

.input:focus {
  border-color: var(--color-primary);
  box-shadow: 0 0 0 3px rgba(37, 99, 235, 0.15);
}
```

### 8. CSS File Organization

Keep your CSS files organized in this order:

```css
/* 1. Variables / Tokens */
/* 2. Reset / Base */
/* 3. Typography */
/* 4. Layout (grid, containers) */
/* 5. Components (buttons, cards, inputs) */
/* 6. Pages / Sections (hero, navbar, footer) */
/* 7. Utilities (text-center, hidden, etc.) */
/* 8. Media Queries */
/* 9. Animations / Keyframes */
```

---

## What NOT to Do

| Avoid | Use Instead |
|---|---|
| Inline styles `style="color:red"` | CSS classes |
| `!important` everywhere | Proper specificity |
| Fixed pixel widths `width: 800px` | Relative units + max-width |
| `<div>` for buttons/links | `<button>`, `<a>` |
| Hardcoded colors `#2563eb` in 50 places | CSS variables |
| Only testing on desktop | Mobile-first + responsive |

---

## Quick Reference — Units to Use

| Use Case | Unit |
|---|---|
| Font sizes | `rem` |
| Spacing / padding / margin | `rem` |
| Borders | `px` |
| Width containers | `%` or `ch` |
| Max widths | `px` |
| Viewport-based sizing | `vw`, `vh`, `svh` |
| Avoid | `em` (unless intentional nesting) |
