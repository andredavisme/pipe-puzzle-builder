# Pipe Puzzle Builder

An interactive 2D drag-and-drop visualizer for assembling galvanized steel pipe projects — like building in-store, but online.

## Features

- **Visual catalog** — all pieces rendered as SVGs with a galvanized steel look (threaded ends, metallic gradient)
- **Relative sizing** — a ½" tee is visibly smaller than a 2" tee
- **Nominal size tabs** — switch ½" through 2"; all pieces rescale instantly
- **Drag & drop canvas** — place pieces, rotate (R key or buttons), flip, delete
- **Live BOM** — running parts count at the bottom
- **Export list** — downloads a plain-text parts list for Home Depot / Lowes
- **Save & share** — writes to Supabase; returns a shareable `?s=<token>` URL
- **Supabase catalog backend** — pieces, sizes, SKUs, and pricing from real Southland/STZ data

## Piece Catalog

| Category | Pieces |
|---|---|
| Pipes | 2", 4", 6", 12", 18", 24", 36" |
| Fittings | Coupling, Cap, 90° Elbow, 45° Elbow, Tee, Cross, Union, Close Nipple |
| Reducers | Hex Bushing, Bell Reducer Coupling |
| Flanges | Floor Flange |

Nominal sizes: ½", ¾", 1", 1¼", 1½", 2"

## Setup

1. Clone this repo
2. Open `index.html` directly in a browser, or deploy to GitHub Pages / Netlify / Cloudflare Pages
3. The Supabase project is pre-configured — no additional setup needed for read-only catalog browsing

## Supabase Schema

| Table | Purpose |
|---|---|
| `pipe_nominal_sizes` | ½"–2" nominal sizes with true ODs |
| `pipe_categories` | Pipes / Fittings / Reducers / Flanges |
| `pipe_pieces` | Size-agnostic piece definitions (18 pieces) |
| `pipe_piece_sizes` | Per-size variant — SKU, price, svg_data (~130 rows) |
| `pipe_assemblies` | Named saved assemblies with share_token |
| `pipe_assembly_pieces` | Canvas placement — x/y/rotation per piece per assembly |

## Brands / SKUs

Catalog is seeded with real **Southland** and **STZ** galvanized steel SKUs sourced from Home Depot product data (approximate retail pricing).

## Deploy

This is a single-file static app. Deploy `index.html` anywhere:

```bash
# GitHub Pages — push to main, enable Pages in repo settings
# Netlify — drag index.html into Netlify drop
# Cloudflare Pages — connect repo, build command: none, publish dir: /
```

## License

MIT
