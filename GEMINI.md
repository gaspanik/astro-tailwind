# Project Design System Rules

This document outlines the architectural and stylistic rules for integrating designs into this codebase, specifically tailored for Astro with Tailwind CSS v4.

## 1. Design System Structure

### Token Definitions
*   **Source of Truth:** Tailwind CSS v4 Default Theme.
*   **Configuration:** No custom `tailwind.config.js` exists. Tokens are derived strictly from Tailwind's defaults.
*   **Typography:**
    *   **Font Family:** `Noto Sans JP` (imported in `src/styles/global.css`).
    *   **Weights:** 400 (Regular) - 700 (Bold).
*   **Colors:** Standard Tailwind palette (e.g., `gray-50`, `gray-600`).
*   **Spacing:** Standard Tailwind spacing scale (e.g., `mt-4` = 1rem, `gap-2` = 0.5rem).

**Code Snippet (`src/styles/global.css`):**
```css
@import url('https://fonts.googleapis.com/css2?family=Noto+Sans+JP:wght@400-700&display=swap');
@import "tailwindcss";
```

## 2. Component Library

*   **Definition:** UI components are defined as `.astro` files in `src/components/`.
*   **Architecture:**
    *   **Single File Components:** Script (frontmatter), Template (HTML), and Styles (optional scoped CSS) are in one file.
    *   **Props:** Defined in the component frontmatter (TypeScript interface recommended).
*   **Usage:** Imported and used directly in pages or layouts.

**Code Snippet (`src/components/Welcome.astro`):**
```astro
---
import { RocketIcon } from '@lucide/astro'
// Props definition (if needed)
// interface Props { title: string; }
---

<div class="flex flex-col ...">
  <RocketIcon class="w-6 h-6" />
  <!-- Content -->
</div>
```

## 3. Frameworks & Libraries

*   **Core Framework:** [Astro](https://astro.build)
*   **Styling Engine:** [Tailwind CSS v4](https://tailwindcss.com)
*   **Icon Library:** [Lucide Icons (Astro)](https://lucide.dev/guide/packages/lucide-astro)
*   **Package Manager:** pnpm
*   **Build Tool:** Vite (internal to Astro)

## 4. Asset Management

*   **Processed Assets (`src/assets/`):**
    *   Images and vectors that require optimization or bundling should be placed here.
    *   Import them in Astro files: `import logo from '../assets/logo.svg';`
*   **Static Assets (`public/`):**
    *   Files that should be served as-is (e.g., `favicon.svg`, `robots.txt`).
    *   Referenced via root-relative paths: `<img src="/favicon.svg" />`

## 5. Icon System

*   **Library:** `@lucide/astro`
*   **Usage:** Import specific icons as components.
*   **Styling:** Style icons using Tailwind classes via the `class` prop (size, color, margin).

**Example:**
```astro
import { HomeIcon } from '@lucide/astro';

<HomeIcon class="w-5 h-5 text-gray-600" />
```

## 6. Styling Approach

*   **Methodology:** Utility-first (Tailwind CSS).
*   **Global Styles:** Minimal. Defined in `src/styles/global.css` (imports fonts and Tailwind).
*   **Component Styles:**
    *   **Primary:** Use Tailwind utility classes directly in HTML (`class="..."`).
    *   **Secondary (if needed):** Use `<style>` tag within `.astro` files for complex or scoped overrides.
*   **Responsive Design:** Use Tailwind's responsive prefixes (`md:`, `lg:`, etc.).

## 7. Project Structure

```text
/
├── src/
│   ├── assets/        # Optimized assets (images, svgs)
│   ├── components/    # Reusable UI components (.astro)
│   ├── layouts/       # Page layouts (wrappers)
│   ├── pages/         # File-based routing endpoints
│   └── styles/        # Global CSS (global.css)
├── public/            # Static assets
├── astro.config.mjs   # Framework config
└── package.json       # Dependencies
```

## Integration Checklist for New Designs

1.  [ ] **Check Tokens:** Does the design use standard Tailwind colors/spacing? If not, map to the closest Tailwind utility or extend the theme (requires creating a config).
2.  [ ] **Identify Components:** Break down the design into reusable Astro components.
3.  [ ] **Assets:** Export images to `src/assets` (if optimization needed) or `public`.
4.  [ ] **Icons:** Find the matching icon in Lucide. Do not export SVGs from Figma if a Lucide equivalent exists.
5.  [ ] **Layout:** Implement using Flexbox/Grid utilities (`flex`, `grid`, `gap-*`).
