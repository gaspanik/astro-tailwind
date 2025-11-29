# Project Context: Astro + Tailwind CSS v4

## 1. Project Overview

This project is a static site generator built with **Astro**, styled using **Tailwind CSS v4**, and maintained with **Biome** for linting and formatting. It serves as a modern, performance-focused web application foundation.

### Key Technologies
*   **Framework:** [Astro](https://astro.build) (v5.x)
*   **Styling:** [Tailwind CSS v4](https://tailwindcss.com) (via `@tailwindcss/vite`)
*   **Linting & Formatting:** [Biome](https://biomejs.dev)
*   **Package Manager:** `pnpm`
*   **Icons:** [Lucide](https://lucide.dev/guide/packages/lucide-astro) (`@lucide/astro`)

## 2. Building and Running

All commands are run via `pnpm`.

### Core Commands
*   **Install Dependencies:** `pnpm install`
*   **Start Development Server:** `pnpm dev` (Runs on `http://localhost:4321`)
*   **Build for Production:** `pnpm build` (Output to `./dist/`)
*   **Preview Production Build:** `pnpm preview`

### Quality Assurance
*   **Lint Code:** `pnpm lint` (Runs `biome lint --write`)
*   **Format Code:** `pnpm format` (Runs `biome format --write`)
*   **Type Check:** `pnpm check` (Runs `astro check`)

## 3. Development Conventions

### File Structure
*   `src/pages/`: File-based routing. Each `.astro` file becomes a route.
*   `src/components/`: Reusable UI components.
*   `src/layouts/`: Wrapper components for pages (e.g., `Layout.astro` defines `<head>` and `<body>`).
*   `src/styles/`: Global styles (e.g., `global.css` for font imports and Tailwind directives).
*   `src/assets/`: Optimized assets (images, SVGs).

### Design System Rules

#### Typography
*   **Font Family:** `Noto Sans JP` (Imported in `src/styles/global.css`).
*   **Base Style:** Applied globally in `src/layouts/Layout.astro`:
    ```css
    html, body {
      font-family: "Noto Sans JP", sans-serif;
    }
    ```

#### Styling (Tailwind CSS v4)
*   **Configuration:** Uses zero-config Tailwind v4. No `tailwind.config.js`.
*   **Directives:** `@import "tailwindcss";` in `src/styles/global.css`.
*   **Approach:** Utility-first. Use classes directly in markup.
*   **Responsive:** Use standard prefixes (`md:`, `lg:`, etc.).

#### Icons
*   **Library:** `@lucide/astro`.
*   **Usage:** Import components directly.
    ```astro
    import { RocketIcon } from '@lucide/astro';
    <RocketIcon class="w-6 h-6 text-blue-500" />
    ```

### Coding Style (Biome)
*   **Indentation:** 2 spaces.
*   **Quotes:** Single quotes for JavaScript/TypeScript.
*   **Semicolons:** As needed (avoid excessive usage where automatic insertion works safely, but follow Biome's specific rules).
*   **Imports:** Organized automatically by Biome.

### Component Architecture
*   **Astro Components:** Prefer `.astro` files.
    *   **Frontmatter:** TypeScript interface for Props.
    *   **Template:** HTML with JSX-like expressions.
    *   **Styles:** Scoped `<style>` blocks are permitted but prefer Tailwind utilities.

### Common Pitfalls
* **Don't** use PostCSS config files - Tailwind v4 uses Vite plugin only
* **Don't** use old Tailwind import syntax (`@tailwind base;` etc.) - use `@import "tailwindcss"` in CSS files
* **Don't** use arbitrary values excessively (e.g., `text-[2rem]`) - prefer standard utilities in v4
* **Don't** import Lucide from `lucide-astro` or `lucide-react` - ALWAYS use `@lucide/astro` (the correct package for this project)
* **Don't** run ESLint/Prettier - use Biome commands exclusively
* **Don't** add semicolons everywhere - Biome uses `asNeeded` mode
* **Don't** import Google Fonts in Layout - already imported in `global.css`
* **Don't** organize imports automatically - Biome has this disabled

## 4. Configuration Files
*   **`astro.config.mjs`:** Main Astro config. Includes `tailwindcss()` Vite plugin.
*   **`biome.json`:** Rules for linter and formatter.
*   **`package.json`:** Scripts and dependencies.
