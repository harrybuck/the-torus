# The Torus

Interactive 3D library visualization for your Obsidian vault.

The Torus turns your vault into a walkable 3D library. Notes become books on shelves, shelves form rooms, rooms form a continuous space organized by topic. A built-in AI librarian (Zero) reads alongside you, surfaces connections across what you've captured, and gardens the vault over time.

## Install (beta)

The Torus is currently distributed via [BRAT](https://github.com/TfTHacker/obsidian42-brat). Community-directory submission is pending.

1. Install BRAT from Obsidian's Community plugins browser.
2. In BRAT: **Add beta plugin** → paste `https://github.com/harrybuck/the-torus` → select latest version → **Add plugin**.
3. On first load, the plugin offers a one-click installer for its search engine and texture pack.

Full setup guidance ships inside the plugin.

## What's in a release

Each release ships:

- `main.js`, `manifest.json`, `styles.css` — the plugin itself
- `qmd-bundle-darwin-arm64.tar.xz`, `qmd-bundle-darwin-x64.tar.xz` — Smart Search engine (Node + qmd), downloaded on user consent
- `textures.tar.gz` — PBR texture pack for the 3D library

The plugin downloads search and texture assets on first run, with consent. Nothing leaves your machine without a click.

## Source

Plugin source is private during the beta. This repository is the public distribution surface.
