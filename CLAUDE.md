# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

A simple browser-based dress-up game for kids. The entire application is a single self-contained HTML file (`www/index.html`) with inline CSS and JavaScript - no build tools, dependencies, or compilation required.

## Running the Game

Open `www/index.html` directly in a browser, or serve the `www/` directory with any static file server:

```bash
python3 -m http.server 8000 -d www
# Then open http://localhost:8000
```

## Architecture

The game is structured as a single-page application in one HTML file:

- **CSS** (lines 7-216): Styles for the game layout, character display, wardrobe panel, and responsive design
- **HTML** (lines 218-278): Game container with character stage and wardrobe panel
- **JavaScript** (lines 280-711): Game logic including:
  - `clothingData` object: All clothing items defined as SVG snippets organized by category (hair, top, bottom, shoes, accessory, hat)
  - `currentOutfit` state: Tracks currently selected items
  - Core functions: `selectItem()`, `resetCharacter()`, `randomOutfit()`, `saveOutfit()`, `loadSavedOutfit()`

## Adding New Clothing Items

Add items to the appropriate category array in `clothingData`. Each item needs:
- `id`: Unique identifier
- `name`: Display name
- `color`: Thumbnail preview color
- `svg`: SVG markup that renders on the character (positioned within a 200x350 viewBox)

Items with `isRemove: true` clear that clothing slot.

## Clothing Layers (z-index order)

1. body-base (z-index: 1) - Base character body
2. slot-skin (z-index: 2)
3. slot-bottom (z-index: 3)
4. slot-top (z-index: 4)
5. slot-shoes (z-index: 5)
6. slot-hair (z-index: 6)
7. slot-accessory (z-index: 7)
8. slot-hat (z-index: 8)
