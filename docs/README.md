# `docs/` — assets for the GitHub README

Drop the following files here so the README renders properly. Until you do,
the top of the README will show broken image links.

## Required images

| Filename | Dimensions | What to capture |
|---|---|---|
| `banner.png` | 1280×640 (or any wide ratio) | Hero banner shown above the README title. Suggested content: poster preview + project title overlay. |
| `screenshot-poster.png` | ~540×810 or 1080×1620 | The champion share poster (the actual PNG the app generates is ideal) |
| `screenshot-bracket.png` | ~900×600 | The knockout bracket view (desktop layout, light or dark) |
| `screenshot-leaderboard.png` | ~900×600 | The stats / top-scorer leaderboard view |

## OG image (for social sharing)

| Filename | Dimensions | Goes where |
|---|---|---|
| `og-image.png` | **1200×630** | Place this in the **repo root** (NOT in `docs/`). Referenced by the `<meta property="og:image">` tag in `index.html`. |

This is what shows up when the live site is shared on Twitter / WeChat / weibo / Facebook etc.

## How to create them

**Easiest path**:

1. Open the live site in a desktop browser at ~1366px width
2. Use the browser's screenshot tool (Chrome DevTools `Cmd/Ctrl + Shift + P` → "Capture full size screenshot") or `Win + Shift + S` on Windows
3. Crop / scale to the dimensions above using any image tool (Preview / Paint / Photopea)
4. Save with the filenames listed above

**For the OG image specifically**:

The app generates a 1080×1620 vertical poster. The OG spec wants 1200×630 (landscape). Two approaches:

- **Option A (simple)**: Take a landscape screenshot of the desktop UI showing the knockout bracket with a champion. Scale to 1200×630.
- **Option B (designed)**: Compose a custom 1200×630 image with the poster on the right, title + tagline on the left. Use any design tool.

## Once you've added them

`git add docs/ og-image.png && git commit -m "docs: add screenshots and OG image"`
