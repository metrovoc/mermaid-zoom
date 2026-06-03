# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Language Convention

- **Code comments** and **git commit messages** must be written in **English**.
- Other text output (docs, descriptions, user-facing strings) should prefer English where practical.

## Project

Fork of [xiaozhuang0433/mermaid-zoom](https://github.com/xiaozhuang0433/mermaid-zoom).
Obsidian plugin: Zoom & Pan for Mermaid diagrams.

## Commands

```bash
npm install
npm run dev    # Watch mode (esbuild, auto-rebuild on change)
npm run build  # Production build (tsc type-check + esbuild minified)
```

There are no tests.

## Architecture

- `main.ts` — single source file, contains all plugin logic (~860 lines)
- `MermaidZoomPlugin` — main class, extends Obsidian `Plugin`
- Diagram detection via `MutationObserver` + Obsidian's `registerMarkdownCodeBlockProcessor`
- Zoom state per diagram stored in `Map<HTMLElement, ZoomState>`
- Lifecycle: `addWheelZoom` / `addDragPan` / `addTouchGestures` / `addResizeHandles` each return a `() => void` cleanup function, registered via `this.register()` for automatic cleanup on plugin unload. Fullscreen modal manages its own cleanup in `closeModal`.
- Build: esbuild → `main.js` (CommonJS), TypeScript strict mode (`noImplicitAny`, `strictNullChecks`)

## Release

GitHub Action (`.github/workflows/release.yml`) builds and releases automatically on push to `main` (paths-ignore: README, LICENSE, manifest.json, package.json). Supports `workflow_dispatch` for manual triggers.
BRAT-compatible: release includes `main.js`, `manifest.json`, `styles.css`.
Version is auto-bumped (patch +1) if the tag already exists. Bump commits use `[skip ci]` to prevent workflow loops.
