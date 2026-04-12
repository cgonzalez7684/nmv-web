# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

```bash
npm run dev       # Start development server (localhost:4321)
npm run build     # Build for production → dist/
npm run preview   # Preview production build locally
```

No test runner or linter is configured.

## Architecture

**Astro static site** deployed to Azure Static Web Apps via GitHub Actions (`.github/workflows/`). No server-side logic — purely static output.

### Routing
File-based routing under `src/pages/`:
- `index.astro` — main landing page (hero, services, quotation modal)
- `index2.astro` — alternate minimal landing page (blueprint theme)

### Layout
`src/layouts/BaseLayout.astro` is the single shared HTML shell. All pages wrap their content in it via `<slot />`. It sets `lang="es"` and imports `src/styles/global.css`.

### Styling
Tailwind CSS v4 via `@tailwindcss/vite` plugin (configured in `astro.config.mjs`). Custom keyframe animations (fadeIn, logoReveal, titleReveal) are defined in `src/styles/global.css`. No `tailwind.config.*` file — v4 uses CSS-first configuration.

### JavaScript
Minimal vanilla JS inline in `.astro` files for modal open/close (classList toggling). No framework components (React, Vue, etc.).

### Assets
Images live in `src/assets/` and are imported as ES modules for Astro's image optimization pipeline. Static files (favicons) go in `public/`.

## Deployment

Push to `main` triggers the Azure Static Web Apps workflow. The build output directory is `dist/`. PRs trigger a preview deployment that is torn down on PR close.
