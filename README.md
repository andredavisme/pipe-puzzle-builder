# Block Thread Notes

**🧩 Live site: [andredavisme.github.io/pipe-puzzle-builder](https://andredavisme.github.io/pipe-puzzle-builder)**

A freeform visual note-taking app built on an SVG canvas. Organize ideas as **blocks** connected by **threads** — each with an ID, title, and description for project tracking and brainstorming.

Built as a branch of [pipe-puzzle-builder](https://github.com/andredavisme/pipe-puzzle-builder), reusing its SVG canvas, pan/zoom, and dark UI patterns.

---

## Quick Start Tutorial

Follow these 8 steps to create your first board:

1. **Name your board** — When the app loads, click **💾 Save**, type a board name, and confirm. This registers the board in your browser's local storage.
2. **Add a block** — Click **`+ Block`** in the toolbar (or press `N`). A new block appears in the center of the canvas.
3. **Edit the block** — Double-click the block to open the edit modal. Fill in:
   - **ID / Tag** — a short identifier like `PROJ-001` or `IDEA-A`
   - **Title** — the block's headline
   - **Description** — supporting detail or notes
   - **Color** — pick a color to categorize visually
4. **Move blocks** — Drag any block to reposition it on the canvas. Pan the canvas by dragging the background. Zoom with the scroll wheel.
5. **Connect two blocks** — Press `C` (or click ⬡ in the toolbar) to enter **Connect mode**. Click block A, then click block B. A bezier thread is drawn between them automatically.
6. **Edit a thread** — Double-click a thread to give it an ID, label (e.g. "leads to", "depends on"), and description.
7. **Save your work** — Click **💾 Save** at any time to update the board in localStorage. You can save multiple boards and switch between them from the **📂 Boards** panel.
8. **Share the board** — Click **🔗 Copy Link**. This encodes the entire board into a URL hash and copies it to your clipboard. Anyone who opens that link will see your exact board — no login required.

**Fit to screen:** Press ⊡ or the fit button to zoom all blocks into view at once.

---

## Features

### Blocks
Blocks are the core building unit. Each block is a draggable rectangular card on the canvas with:
- A user-defined **ID / Tag** for categorization (e.g. `PROJ-001`, `MILESTONE-3`)
- A **Title** shown on the face of the block
- A **Description** for longer notes and context
- A **Color** for visual grouping or priority coding

Double-click any block to edit all four fields. Press `Delete` or `Backspace` to remove the selected block (its threads are removed automatically).

### Threads
Threads are bezier curves that connect two blocks, representing a relationship or dependency. Each thread has:
- An **ID / Tag** for identification
- A **Label** describing the relationship (e.g. "leads to", "blocks", "references")
- A **Description** for additional notes
- An **Arrowhead** showing direction from source to target

Switch to Connect mode (`C`), click the source block, then click the target block. The thread snaps to the nearest edge ports for a clean curve. Double-click any thread to edit it.

### Connect Mode
Toggle between **Select mode** (`V`) and **Connect mode** (`C`). In Connect mode, clicking a block begins a thread; clicking a second block completes it. Press `Esc` to cancel mid-connection.

### Canvas Controls
- **Pan** — drag the background to move around the canvas
- **Zoom** — scroll wheel to zoom in and out
- **Fit to screen** — ⊡ button scales and centers all blocks in view
- **Delete** — `Delete` or `Backspace` removes the selected block or thread

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

## Saving & Sharing

### How data is saved

There are two independent mechanisms:

| Method | Where data lives | Survives browser close? | Cross-browser? | Backup-safe? |
|---|---|---|---|---|
| 💾 **Save button** | `localStorage` in that browser | ✅ Yes | ❌ No | ❌ No |
| 🔗 **Copy Link** | URL hash — no storage at all | N/A | ✅ Yes | ✅ Yes (save the URL) |

### What "browser-specific" means
If you save a board in Chrome and later open Firefox (or an Incognito window), your saved boards won't appear — they only exist in the exact browser profile where you saved them. The **Copy Link** button solves this: the link carries the full board state, so it opens identically in any browser, device, or private session.

### Backup your work
Right now the safest backup is your **share link** — copy it and store it somewhere (notes app, email, bookmark). Treat it like a save file.

**Coming soon:**
- 📥 **Export to JSON** — download the full board as a `.json` file you can re-import later
- 📊 **Export to CSV** — two files (`blocks.csv` and `threads.csv`) in a relational schema ready for database import
- 📤 **Import from JSON** — drag-drop or file-picker to restore a board from a backup

---

## Data Model

### Board (URL hash / localStorage)
```json
{
  "name": "My Project Board",
  "blocks": [...],
  "threads": [...]
}
```

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
