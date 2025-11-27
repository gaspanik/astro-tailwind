# Copilot Instructions for Astro + Tailwind CSS + Biome Project

## Architecture Overview

This is an Astro static site project using **Tailwind CSS v4** (latest version with Vite plugin), Biome for linting/formatting, and Lucide for icons. The project is Japanese-focused with Noto Sans JP as the default font.

### Key Technology Decisions

- **Tailwind v4**: Uses `@tailwindcss/vite` plugin configured in `astro.config.mjs`, not PostCSS. Import via `@import "tailwindcss"` in `src/styles/global.css`
- **Biome over ESLint/Prettier**: All code quality handled by Biome with strict configuration
- **pnpm**: Package manager with workspace configuration (`pnpm-workspace.yaml` optimizes esbuild/sharp builds)
- **mise**: Development environment manager (Node 24) with task runner shortcuts

## Code Style & Conventions

### Biome Configuration (`biome.json`)

- **Formatting**: 2-space indent, 80-char line width, single quotes for JS, double quotes for JSX/CSS
- **JavaScript**: Trailing commas everywhere, semicolons only when needed (`asNeeded`)
- **Astro files**: Unused imports/variables allowed (disable `noUnusedImports`, `noUnusedVariables`)
- **CSS**: Tailwind directives parsing enabled

### Component Patterns

**Layout Structure** (`src/layouts/Layout.astro`):
- Import `../styles/global.css` for Tailwind
- Include Noto Sans JP from Google Fonts
- Reset margin/padding in scoped `<style>` tags
- Accept `title` prop with default value

**Component Example** (`src/components/Welcome.astro`):
```astro
---
import { SquareDashed } from '@lucide/astro'
---
<div class="flex flex-col justify-center items-center bg-gray-100 min-h-screen">
  <div class="flex items-center gap-2 mt-4">
    <SquareDashed class="w-6 h-6" />
    <h1 class="font-semibold text-2xl">Hello world!</h1>
  </div>
</div>
```

**Icons**: Use `@lucide/astro` imports, not `lucide-react`. Apply Tailwind classes directly to icon components.

## Development Workflows

### Essential Commands

- **Dev server**: `pnpm dev` (localhost:4321)
- **Build**: `pnpm build` → `./dist/`
- **Code quality**: `pnpm check` (lint + format + fix in one command)
- **Mise tasks**: `mise run astro:dev`, `mise run biome:check` (with confirmation prompts)

### Adding Dependencies

Use `pnpm add <package>` (not npm/yarn). For build-heavy packages (esbuild, sharp), they're already configured in `pnpm-workspace.yaml` to only build dependencies.

### Creating New Components

1. Place in `src/components/` with `.astro` extension
2. Import Lucide icons from `@lucide/astro`
3. Use Tailwind utility classes directly (no CSS modules)
4. Run `pnpm check` before committing to auto-fix formatting

### TypeScript Configuration

- Uses Astro's strict tsconfig (`astro/tsconfigs/strict`)
- Includes `.astro/types.d.ts` for type generation
- Excludes `dist/` directory

## Common Pitfalls

- **Don't** use PostCSS config files - Tailwind v4 uses Vite plugin only
- **Don't** import Lucide from `lucide-react` - use `@lucide/astro`
- **Don't** run ESLint/Prettier - use Biome commands exclusively
- **Don't** format Astro files with external formatters - Biome handles it with special rules
- **Don't** add semicolons everywhere - Biome uses `asNeeded` mode

## Integration Points

- **Vite**: Tailwind CSS v4 plugin configured in `astro.config.mjs`
- **Git**: Biome respects `.gitignore` via `vcs.useIgnoreFile: true`
- **Fonts**: Google Fonts linked in `Layout.astro` (Noto Sans JP for Japanese support)

## File Organization

- Pages → `src/pages/` (Astro file-based routing)
- Components → `src/components/` (reusable `.astro` components)
- Layouts → `src/layouts/` (page templates)
- Styles → `src/styles/global.css` (Tailwind imports only)
- Static assets → `public/` (served as-is)
