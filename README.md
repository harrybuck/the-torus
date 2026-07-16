# The Torus

A second-brain package, with 3D library visualization, AI-assisted note enrichment, search, and a memory harness for external AIs (e.g. Claude Desktop, Codex).

The Torus turns notes you choose into a walkable 3D library — notes become books on shelves, shelves form rooms, rooms form a continuous space organized by topic. It pairs that with a capture pipeline that pulls in messages, email, and web content and enriches them, and it exposes your curated knowledge to an external AI assistant as a durable memory it can read, search, and reason over across sessions.

**Desktop only.** The plugin uses Node APIs (file access outside the vault, subprocesses) that aren't available on mobile.

## Install (beta)

The Torus is currently distributed via [BRAT](https://github.com/TfTHacker/obsidian42-brat). Community-directory submission is pending.

1. Install BRAT from Obsidian's Community plugins browser.
2. In BRAT: **Add beta plugin** → paste `https://github.com/harrybuck/the-torus` → select the latest version → **Add plugin**.
3. On first load, the plugin offers one-click installers for its optional search engine and texture pack.

Full setup guidance ships inside the plugin. Run **Torus: Run diagnostics** at any time for a report on what's actually working.

## Requirements

- **Obsidian 1.0+ on desktop** (macOS primarily; the iMessage and WhatsApp capture features are macOS-only).
- Everything below is **optional and opt-in**. The core — the 3D library, note membership, and built-in keyword search — works with no external dependencies, no downloads, and no accounts.

---

## Disclosures

Read this before installing. The Torus does more than render a library, and all of it is listed here.

### Network usage

- **Optional component downloads.** On an explicit click (never automatically, never on load), the plugin can download from this repository's releases:
  - the **Torus Search** engine bundle — [qmd](https://github.com/tobi/qmd) plus a Node.js runtime and native search modules (**~60 MB** Apple Silicon, **~70 MB** Intel),
  - the **WhatsApp bridge** bundle — Chromium plus a Node.js runtime (**~145 MB** Apple Silicon, **~160 MB** Intel),
  - **3D textures** for the library (**~26 MB**).

  Each download is verified against a SHA-256 checksum compiled into the plugin. You are asked first; declining leaves the plugin fully functional with built-in keyword search.
- **Embedding models.** If you enable semantic search, the search engine downloads models from HuggingFace on first index (~300 MB, and up to ~1.8 GB if reranking and query expansion are used).
- **Content you ask it to capture.** Fetching a URL retrieves that page — via [defuddle](https://github.com/kepano/defuddle), with Jina Reader as a fallback — plus YouTube transcripts and X/Twitter posts (through the X API if you supply your own bearer token, otherwise FxTwitter).
- **Your email server**, if you enable email capture (IMAP).
- **Local-only listeners.** The plugin runs an MCP server bound to `127.0.0.1` and token-gated, and the WhatsApp bridge exposes a local health endpoint. Neither is reachable from outside your machine.
- **No analytics, no telemetry, no ads.** Nothing about your vault or your usage is sent anywhere except the services you explicitly configure above.

### File access outside your vault

- `~/Library/Messages/chat.db` — **read-only**, and **only if you enable iMessage capture**. Requires granting Obsidian Full Disk Access in macOS System Settings. macOS only.
- `~/.claude/` — reads Claude Code session transcripts to build the assistant's memory, only if you use the Claude Code integration.
- **The plugin's own data folder** — downloaded bundles, the search index database, and WhatsApp session credentials.
- **Subprocesses.** For features you enable, the plugin runs: the search engine, the WhatsApp bridge, `git`, and the `claude` CLI. It executes only components it ships or that you have installed yourself; it does not fetch and run arbitrary code.

### Accounts and payment

- **The AI assistant features require a paid [Claude Code](https://claude.com/claude-code) subscription** (Anthropic). Authentication is through your existing Claude Code login — the plugin does not ask for or store an API key. Without a subscription, the 3D library, note membership, capture, and search all still work; the conversational assistant does not.
- **WhatsApp capture** requires pairing your own WhatsApp account by scanning a QR code.
- **Email capture** requires your own IMAP credentials, stored locally in plugin settings.
- **X/Twitter thread capture** optionally uses your own X API bearer token.

### Third-party components

All bundled components are open source, shipped prebuilt:

| Component | License | Source |
|---|---|---|
| qmd (search engine) | MIT | [github.com/tobi/qmd](https://github.com/tobi/qmd) — © Tobi Lutke |
| Node.js runtime | MIT | [nodejs.org](https://nodejs.org) |
| Chromium (WhatsApp bridge) | BSD-3-Clause | via whatsapp-web.js / Puppeteer |

No closed-source code is included.

---

## Search: two tiers

- **Built-in keyword search** — pure JavaScript, always available, no downloads, no dependencies. Indexes only the notes you've added to The Torus. This is the default and it's sufficient for typical vaults.
- **Torus Search (optional upgrade)** — adds semantic and hybrid search, and scales to large collections. Recommended above roughly 1,000 notes in The Torus.

If you already have `qmd` installed, The Torus detects and uses it — nothing is downloaded. If you don't, install the bundle with one click, or install it yourself with `npm install -g @tobilu/qmd` (requires Node.js).

Only one engine answers any given search — results are never blended.

## Memory harness for external AIs

The Torus exposes your curated notes to an external AI assistant — Claude Desktop, Codex, or any MCP-capable client — as a persistent memory it can read, search, and reason over across sessions, instead of starting cold every conversation.

The plugin runs an MCP server bound to `127.0.0.1`, gated behind a token written to your local config. It isn't reachable from outside your machine, and it serves only the notes you've added to The Torus. Which assistant you point at it — or whether you run one at all — is entirely your choice.

## Membership: your notes, where they already are

Notes become part of The Torus through frontmatter (`torus_status`), not location. Adopting a note doesn't move or copy it — the file stays exactly where you put it. Nothing in your vault is indexed or displayed unless you explicitly add it.

Commands: **Add to Torus**, **Add Directory to Torus**, **Eject from Torus**.

## What's in a release

- `main.js`, `manifest.json`, `styles.css` — the plugin itself
- `qmd-bundle-darwin-arm64.tar.xz`, `qmd-bundle-darwin-x64.tar.xz` — Torus Search engine (Node + qmd), downloaded on consent
- `bridge-bundle-darwin-arm64.tar.xz`, `bridge-bundle-darwin-x64.tar.xz` — WhatsApp bridge (Node + Chromium), downloaded on consent
- `textures.tar.gz` — PBR texture pack for the 3D library

Every optional download is consent-gated and SHA-256 verified. Nothing leaves your machine without a click.

## Source

Plugin source is private during the beta. This repository is the public distribution surface.

## License

MIT — see [LICENSE](LICENSE).
