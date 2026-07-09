# Mermaid Zoom

[English](README.md) | [简体中文](README.zh-CN.md)

An Obsidian plugin that adds zoom and pan functionality to Mermaid diagrams.

![Version](https://img.shields.io/badge/dynamic/json?url=https%3A%2F%2Fraw.githubusercontent.com%2Fxiaozhuang0433%2Fmermaid-zoom%2Fmain%2Fmanifest.json&query=$.version&prefix=v&label=version&color=2D9CDB)
![License](https://img.shields.io/badge/license-MIT-blue.svg)

## Features

- **Optional Mouse Wheel Zoom** - Enable wheel zoom per diagram when you want scroll-to-zoom
- **Drag to Pan** - Click and drag to move around your diagrams
- **Touch Gestures** - Pinch to zoom and drag to pan on mobile devices
- **Compact Controls** - Reveal zoom controls from a small bottom-right control
- **Scale Indicator** - Display the current zoom level in the compact controls
- **Fullscreen Mode** - Open diagrams in a modal for better viewing

## Installation

### Obsidian Plugin Market (Coming Soon)

Once approved, install directly from Obsidian's community plugins browser.

### Manual Installation

1. Download the latest release from [GitHub Releases](https://github.com/xiaozhuang0433/mermaid-zoom/releases)
2. Extract to your vault's plugins directory:
   ```
   <your-vault>/.obsidian/plugins/mermaid-zoom
   ```
3. Enable the plugin in Obsidian:
   - Settings → Community Plugins
   - Find "Mermaid Zoom" and enable it

## Usage

### Mouse Controls

| Action | Description |
|--------|-------------|
| **Wheel zoom** | Open the compact controls, enable Wheel, then scroll over the diagram |
| **Pan** | Click and drag to move the diagram |
| **Fullscreen** | Open the compact controls and click the fullscreen button |

### Touch Controls (Mobile)

| Action | Description |
|--------|-------------|
| **Zoom** | Pinch with two fingers |
| **Pan** | Drag with one finger |

### Compact Controls

Hover, focus, or click the bottom-right control to reveal:

- Current zoom level
- Zoom out
- Zoom in
- Fit diagram
- Wheel zoom button
- Fullscreen

## Development

```bash
# Install dependencies
npm install

# Development mode (watch for changes)
npm run dev

# Production build
npm run build
```

## How It Works

The plugin automatically detects all Mermaid diagrams rendered in Obsidian and wraps each one in a zoomable container. Zoom range is configurable from 10% to 500%.

Original SVG dimensions are cached to ensure consistent scaling behavior when resetting or resizing.

## License

[MIT](LICENSE) © [Wang Xiao Zhuang](https://github.com/xiaozhuang0433)

## Support

- Issues: [GitHub Issues](https://github.com/xiaozhuang0433/mermaid-zoom/issues)
- Discussions: [GitHub Discussions](https://github.com/xiaozhuang0433/mermaid-zoom/discussions)
