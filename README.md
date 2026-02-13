# Sticker PDF Lab

A browser-based PDF editor with:

- Text insertion
- Font selection for added text
- `Edit Text` mode that auto-detects PDF text boxes per page
- OCR mode (`Tesseract.js`) for scanned/image-only PDFs
- Freehand drawing
- Shapes (rectangle, ellipse, line) with color and opacity controls
- Layer controls (bring front / send back)
- Duplicate, delete, clear-page actions
- Undo/redo
- Multi-page support with thumbnail navigation
- Export back to PDF
- Split/extract page ranges from the edited PDF

## Run

1. Open a terminal in this folder.
2. Start a local server:

```bash
python3 -m http.server 8080
```

3. Open [http://localhost:8080](http://localhost:8080).
4. Upload a PDF and edit.
5. Click **Export PDF** to download the edited file.
6. Optional: add split ranges and click **Split / Extract**.
   - `From 3` and `To 5` + **Add Range** extracts pages 3-5.

## Deploy (No Localhost)

### Push To `rukasarasina/billpdfeditor`

Use these exact commands:

```bash
cd "/Users/suhyun/Documents/New project"
git init
git add .
git commit -m "Final polish before upload"
git branch -M main
git remote remove origin 2>/dev/null || true
git remote add origin https://github.com/rukasarasina/billpdfeditor.git
git push -u origin main
```

If GitHub says the remote already has commits, run:

```bash
git pull origin main --allow-unrelated-histories
git push -u origin main
```

Option 1: Netlify Drop (fastest)
1. Open https://app.netlify.com/drop
2. Drag the entire folder (`index.html`, `app.js`, `styles.css`, `README.md`) into the drop area.
3. Netlify gives you a public URL immediately.

Option 2: GitHub Pages
1. Create a new empty repository on GitHub (for example `pdf-editor`).
2. In terminal, run:

```bash
cd "/Users/suhyun/Documents/New project"
git init
git add .
git commit -m "Initial PDF editor"
git branch -M main
git remote add origin https://github.com/<your-username>/pdf-editor.git
git push -u origin main
```

3. On GitHub, open your repo and go to **Settings > Pages**.
4. Under **Build and deployment**, set:
   - Source: `Deploy from a branch`
   - Branch: `main`
   - Folder: `/ (root)`
5. Click **Save**.
6. Wait 1-3 minutes. GitHub shows a public URL like:
   `https://<your-username>.github.io/pdf-editor/`
7. Open that URL and hard refresh once.
8. For updates later, run:

```bash
git add .
git commit -m "Update editor"
git push
```

GitHub Pages auto-redeploys each push.

## Notes

- In `Edit Text` mode:
  - every detected text item gets a selectable box
  - drag any detected box to move it, and the original location is masked live
  - double-click a box to edit inline directly in-place (typing stays inside that text box)
  - press `Enter` or `Esc` to apply the edit
  - use arrow keys to nudge selected text boxes (`Shift + Arrow` moves by 10px)
  - press `Delete` to remove text (masked in export)
- Edited text now preserves original font styling and keeps original size first, expanding box width before shrinking.
- Use the `OCR` button for scanned/image-only PDFs before editing text.
- Original PDF text streams are not rewritten directly; visual edits are flattened into the exported PDF.
- Export uses WYSIWYG raster flattening so the downloaded PDF matches what you see on the page.
- Page rendering scale auto-fits to the stage width so full pages are visible at normal browser zoom.

## Shortcuts

- `V` Select
- `D` Draw
- `T` Text
- `R` Edit Text mode
- `O` Run OCR
- `Delete` / `Backspace` Delete selected object
- `Arrow keys` Nudge selected text box in Edit Text mode
- `Shift + Arrow keys` Nudge by 10px
- `Cmd/Ctrl + Z` Undo
- `Cmd/Ctrl + Shift + Z` Redo
- `Cmd/Ctrl + Y` Redo
