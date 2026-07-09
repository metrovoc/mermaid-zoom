# Mermaid Auto-Fit Issue

## Symptom

Mermaid Zoom no longer consistently auto-fits rendered Mermaid diagrams to an appropriate size in Obsidian Reading mode. This differs from the behavior observed immediately after installing the plugin.

## What We Checked

- The active vault plugin is Mermaid Zoom `1.2.0`.
- Local `manifest.json` and `styles.css` match the GitHub `1.2.0` release.
- Local `main.js` only differs from the release asset by a trailing `/* nosourcemap */` comment.
- Better Copy no longer contains any Mermaid-specific code and does not touch Mermaid DOM.

## Current Hypothesis

This appears to be an independent Mermaid Zoom lifecycle/measurement issue rather than a Better Copy regression.

The plugin measures SVG size with `getBoundingClientRect()` while wrapping the Mermaid SVG, stores that as `svgOriginalWidth` / `svgOriginalHeight`, and later fits using the cached dimensions. Its `ResizeObserver` watches the outer zoom container, but not the SVG's own rendered size or viewBox. If Obsidian/Mermaid finalizes SVG layout after the initial measurement, or if theme/layout changes affect the SVG after wrapping, the cached size can be stale and the fit calculation becomes inaccurate.

## Candidate Fix

- Measure intrinsic SVG size from `viewBox` first.
- Fall back to `getBBox()` when possible.
- Use `getBoundingClientRect()` only as the final fallback.
- Re-measure before each fit instead of relying only on initial cached dimensions.
- Schedule an additional initial fit with `requestAnimationFrame()` after wrapping.
