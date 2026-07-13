# Block Thread Notes

**🧩 Live site: [andredavisme.github.io/pipe-puzzle-builder](https://andredavisme.github.io/pipe-puzzle-builder)**

A freeform visual note-taking app built on an SVG canvas. Organize ideas as **blocks** connected by **threads** — each with an ID, title, and description for project tracking and brainstorming.

Built as a branch of [pipe-puzzle-builder](https://github.com/andredavisme/pipe-puzzle-builder), reusing its SVG canvas, pan/zoom, and dark UI patterns.

---

## Features

- **Blocks** — draggable cards with ID/tag, title, description, and color
- **Threads** — bezier curves connecting blocks, each with its own ID and label
- **Connect mode** — click two blocks to draw a thread between them (auto port selection)
- **Arrowheads** — threads show direction
- **Double-click to edit** — opens a modal for any block or thread
- **localStorage save/load** — boards persist in the browser; browse and restore from the Boards panel
- **Copy Link** — base64-encodes the full board state into a URL hash for zero-dependency sharing
- **Import from link** — opening a shared URL auto-loads the board
- **Fit to screen** — centers and scales all blocks into view
- **Keyboard shortcuts** — see below
- **Dot-grid canvas** — same aesthetic as Pipe Puzzle Builder

---

## Keyboard Shortcuts

| Key | Action |
|---|---|
| `V` | Select / move tool |
| `C` | Connect tool |
| `N` | Add new block |
| `Enter` | Edit selected block or thread |
| `Delete` / `Backspace` | Delete selected block or thread |
| `Esc` | Deselect / cancel connect |
| Scroll wheel | Zoom in / out |
| Drag background | Pan canvas |

---

## Data Model

### Block
```json
{
  "id": "b1k3x9",
  "tag": "PROJ-001",
  "label": "Research Phase",
  "desc": "Gather requirements and competitive analysis",
  "x": 120, "y": 80, "w": 160, "h": 70,
  "color": "#0f3460"
}
```

### Thread
```json
{
  "id": "tabc123",
  "tag": "LINK-001",
  "label": "leads to",
  "desc": "Research feeds directly into planning",
  "fromId": "b1k3x9",
  "toId": "bxyz456"
}
```

---

## Storage

| Method | How it works |
|---|---|
| **localStorage** | Boards saved by name in the browser; persistent across sessions |
| **URL hash export** | Full board state base64-encoded into `#b=...`; copy/paste to share |

No backend, no API keys, no dependencies — fully static.

---

## Deploy

Single `index.html` — works anywhere static files are served:

```bash
# GitHub Pages — workflow in .github/workflows/deploy-block-thread-notes.yml
# Netlify      — drag block-thread-notes/index.html into Netlify drop
# Cloudflare   — connect repo, publish dir: block-thread-notes
```

---

## Related

- **[Pipe Puzzle Builder](https://github.com/andredavisme/pipe-puzzle-builder/tree/main)** — the parent project; drag-and-drop pipe fitting visualizer with Supabase catalog backend

---

## License

MIT
