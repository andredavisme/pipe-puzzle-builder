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
5. **Connect two blocks** — Press `C` (or click the connect button) to enter **Connect mode**. Click block A, then click block B. A bezier thread is drawn between them automatically.
6. **Edit a thread** — Double-click a thread to give it an ID, label (e.g. "leads to", "depends on"), and description.
7. **Save your work** — Click **💾 Save** at any time to update the board in localStorage. You can save multiple boards and switch between them from the **📂 Boards** panel.
8. **Share or back up the board** — Click **🔗 Copy Link** for a live share link, or **📥 Export JSON** for a downloadable backup file.

**Fit to screen:** Press **⊡ Fit** to zoom all blocks into view at once.

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

There are now **four ways** to save or share a board:

| Method | Where data lives | Survives browser close? | Cross-browser? | Backup-safe? |
|---|---|---|---|---|
| 💾 **Save button** | `localStorage` in that browser | ✅ Yes | ❌ No | ❌ No |
| 🔗 **Copy Link** | URL hash — no storage at all | N/A | ✅ Yes | ✅ Yes (save the URL) |
| 📥 **Export JSON** | Downloaded `.json` file | ✅ Yes | ✅ Yes | ✅ Yes |
| 📊 **Export CSV** | Downloaded `blocks.csv` + `threads.csv` | ✅ Yes | ✅ Yes | ✅ Yes |

### What "browser-specific" means
If you save a board in Chrome and later open Firefox (or an Incognito window), your saved boards won't appear — they only exist in the exact browser profile where you saved them. **Copy Link**, **Export JSON**, and **Export CSV** all solve this, since the data travels with the link or file rather than staying in browser storage.

### Backing up your work
- **Quick backup:** Click **📥 Export JSON** to download the full board as a `.json` file. Use **📤 Import JSON** later (any browser, any machine) to restore it exactly.
- **Database seeding:** Click **📊 Export CSV** to download `blocks.csv` and `threads.csv`. These map directly to relational tables and can be imported into Supabase, PostgreSQL, or any SQL database with no transformation.
- **Share link:** Still available via **🔗 Copy Link** for lightweight, no-download sharing.

---

## Data Model

### Board (URL hash / localStorage / JSON export)
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

### CSV Schema

**`blocks.csv`**

**`threads.csv`**
---

## Repo Structure

This branch contains two `index.html` files:

- **Root `index.html`** — the original pipe-puzzle-builder app, inherited when this branch was created from `main`. Not used by this app's deploy workflow.
- **`block-thread-notes/index.html`** — the actual note-taking app. This is the only file the deploy workflow publishes.

---

## Deploy

Single `index.html` — works anywhere static files are served:

```bash
# GitHub Pages — workflow in .github/workflows/deploy-block-thread-notes.yml
# Netlify      — drag block-thread-notes/index.html into Netlify drop
# Cloudflare   — connect repo, publish dir: block-thread-notes
```

### Troubleshooting Deployment

If a GitHub Actions run fails with:
> "Branch 'block-thread-notes' is not allowed to deploy to github-pages due to environment protection rules."

Fix it by allowing this branch to deploy:

1. Go to **Settings → Environments → github-pages**
2. Under **Deployment branches and tags**, click **Add deployment branch rule**
3. Add `block-thread-notes` (or switch to **All branches**)
4. Re-run the failed workflow from the **Actions** tab

---

## Related

- **[Pipe Puzzle Builder](https://github.com/andredavisme/pipe-puzzle-builder/tree/main)** — the parent project; drag-and-drop pipe fitting visualizer with Supabase catalog backend

---

## License

MIT
