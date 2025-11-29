# Copilot Instructions for Astro + Tailwind CSS + Biome Project

## Architecture Overview

This is an Astro static site project using **Tailwind CSS v4** (latest version with Vite plugin), Biome for linting/formatting, and Lucide for icons via `@lucide/astro` package. The project is Japanese-focused with Noto Sans JP as the default font.

### Key Technology Decisions

- **Tailwind v4**: Uses `@tailwindcss/vite` plugin configured in `astro.config.mjs`, not PostCSS. Import via `@import "tailwindcss"` in `src/styles/global.css`
- **Biome over ESLint/Prettier**: All code quality handled by Biome with strict configuration
- **pnpm**: Package manager with workspace configuration (`pnpm-workspace.yaml` optimizes esbuild/sharp builds)
- **mise**: Development environment manager (Node 24) with task runner shortcuts

## Code Style & Conventions

### Biome Configuration (`biome.json`)

- **Formatting**: 2-space indent, 80-char line width, single quotes for JS, double quotes for JSX/CSS
- **JavaScript**: Trailing commas everywhere, semicolons only when needed (`asNeeded`)
- **CSS**: Tailwind directives parsing enabled
- **HTML**: Experimental full support enabled, self-closing void elements always
- **Organize imports**: Disabled (`organizeImports: "off"`)

### Component Patterns

**Layout Structure** (`src/layouts/Layout.astro`):
- Import `../styles/global.css` for Tailwind
- Google Fonts imported in `global.css` (Noto Sans JP with 400-700 weights)
- Reset margin/padding/width/height in scoped `<style>` tags
- Accept `title` prop with default value `'Astro Basics w/ Tailwind CSS'`

**Component Example** (`src/components/Welcome.astro`):
```astro
---
import { RocketIcon } from '@lucide/astro'
---
<div class="flex flex-col justify-center bg-gray-50 min-h-screen align-center">
  <div class="flex flex-col items-start mx-auto">
    <div class="flex items-center gap-2 mt-4">
      <RocketIcon class="w-6 h-6" />
      <h1 class="font-medium text-2xl">Hello astro!</h1>
    </div>
  </div>
</div>
```

**Tailwind CSS v4 Class Names**: CRITICAL - This project uses Tailwind CSS v4 with NEW syntax. Always use the v4 format:
- ✅ `text-2xl` (correct v4 syntax)
- ❌ `text-[2rem]` (avoid arbitrary values unless necessary)
- ✅ `bg-gray-50` (use semantic color scale)
- ❌ `bg-gray-100/50` (old opacity syntax - use `bg-gray-50` instead)
- ✅ Standard utility classes work the same in v4

Key v4 changes to remember:
- Import Tailwind with `@import "tailwindcss"` (not `@tailwind base/components/utilities`)
- Use semantic spacing/sizing (existing utilities work the same)
- Avoid arbitrary values `[]` unless absolutely necessary
- Use standard color scales (`gray-50`, `blue-500`, etc.)

**Icons**: CRITICAL - Always use `@lucide/astro` for imports (e.g., `import { RocketIcon } from '@lucide/astro'`). Never use `lucide-astro` or `lucide-react`. Apply Tailwind classes directly to icon components.

**Page Pattern** (`src/pages/index.astro`): Import components and layouts, wrap components in Layout

## Development Workflows

### Essential Commands

- **Dev server**: `pnpm dev` (localhost:4321)
- **Build**: `pnpm build` → `./dist/`
- **Preview**: `pnpm preview` (preview production build)
- **Check**: `pnpm check` (runs `astro check` for TypeScript validation including `.astro` files)
- **Lint**: `pnpm lint` (runs `biome lint --write` - note: Biome does not check `.astro` files)
- **Format**: `pnpm format` (runs `biome format --write`)

### Mise Task Shortcuts

Available via `mise run <task>` (requires confirmation for destructive operations):
- `astro:dev` - Start dev server
- `astro:build` - Build project (with confirmation)
- `astro:preview` - Preview build (auto-runs build first)
- `astro:upgrade` - Upgrade Astro via `pnpx @astrojs/upgrade`
- `astro:check` - Run Astro TypeScript check
- `biome:format` - Format src/ (with confirmation)
- `biome:lint` - Lint src/ (with confirmation)

### Adding Dependencies

Use `pnpm add <package>` (not npm/yarn). For build-heavy packages (esbuild, sharp), they're already configured in `pnpm-workspace.yaml` with `onlyBuiltDependencies` to optimize installation.

### Creating New Components

1. Place in `src/components/` with `.astro` extension
2. Import Lucide icons from `@lucide/astro` (NOT `lucide-astro`)
3. Use Tailwind utility classes directly (no CSS modules)
4. Run `pnpm check` for TypeScript validation (including `.astro` files), `pnpm lint` and `pnpm format` for JS/TS/CSS quality

### TypeScript Configuration

- Uses Astro's strict tsconfig (`astro/tsconfigs/strict`)
- Includes `.astro/types.d.ts` for type generation
- Excludes `dist/` directory

## Common Pitfalls

- **Don't** use PostCSS config files - Tailwind v4 uses Vite plugin only
- **Don't** use old Tailwind import syntax (`@tailwind base;` etc.) - use `@import "tailwindcss"` in CSS files
- **Don't** use arbitrary values excessively (e.g., `text-[2rem]`) - prefer standard utilities in v4
- **Don't** import Lucide from `lucide-astro` or `lucide-react` - ALWAYS use `@lucide/astro` (the correct package for this project)
- **Don't** run ESLint/Prettier - use Biome commands exclusively
- **Don't** add semicolons everywhere - Biome uses `asNeeded` mode
- **Don't** import Google Fonts in Layout - already imported in `global.css`
- **Don't** organize imports automatically - Biome has this disabled

## Integration Points

- **Vite**: Tailwind CSS v4 plugin configured in `astro.config.mjs`
- **Git**: Biome respects `.gitignore` via `vcs.useIgnoreFile: true`
- **Fonts**: Google Fonts imported in `src/styles/global.css` (Noto Sans JP for Japanese support)
- **TypeScript**: Strict mode via Astro's tsconfig presets

## File Organization

- Pages → `src/pages/` (Astro file-based routing)
- Components → `src/components/` (reusable `.astro` components)
- Layouts → `src/layouts/` (page templates)
- Styles → `src/styles/global.css` (Google Fonts + Tailwind imports only)
- Static assets → `public/` (served as-is)
- Assets → `src/assets/` (processed assets like images/SVGs)
