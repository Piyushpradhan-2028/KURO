[Uploading README (2).md…]()
# KURO — My Daily Journal

A personal, black-and-white anime/manga-inspired daily journal. Single self-contained file — no build tools, no npm install, no backend. Runs entirely in your browser and saves your notes, tasks, and goals to `localStorage`.

## What you have

```
kuro.html   ← the entire app (HTML + CSS + JS in one file)
```

That's it. There's no `package.json`, no `node_modules`, no dev server required to use the app.

## Option 1 — Just open it (fastest)

1. Download `kuro.html` to your computer.
2. Double-click it, or drag it into any browser window (Chrome, Edge, Firefox, Safari).

That's a fully working copy of KURO. The only downside to opening it this way is that some browsers restrict certain features on `file://` pages — this app doesn't use any of those, so it's safe, but running it through a local server (below) is still the more "developer" way to do it and avoids any edge-case browser warnings.

## Option 2 — Run it in VS Code with Live Server (recommended)

This gives you hot-reload if you want to edit the code, and serves the file over `http://localhost` instead of `file://`.

**Step 1 — Install VS Code**
If you don't have it: https://code.visualstudio.com/

**Step 2 — Put the file in a folder**
Create a folder anywhere on your computer, e.g. `kuro-journal/`, and put `kuro.html` inside it.

**Step 3 — Open the folder in VS Code**
- Launch VS Code
- `File → Open Folder...` → select `kuro-journal/`

**Step 4 — Install the "Live Server" extension**
- Click the Extensions icon in the left sidebar (or press `Ctrl+Shift+X` / `Cmd+Shift+X`)
- Search for **Live Server** (by Ritwick Dey)
- Click **Install**

**Step 5 — Launch it**
- Right-click `kuro.html` in the VS Code file explorer
- Choose **"Open with Live Server"**
- Your browser opens automatically at something like `http://127.0.0.1:5500/kuro.html`

The page will now auto-reload any time you save changes to the file — useful if you want to tweak colors, copy, or add features.

## Option 3 — Any other local server

If you don't want to use the Live Server extension, any static file server works, since KURO has zero dependencies. From a terminal, inside the folder containing `kuro.html`:

```bash
# Python 3 (built into most systems)
python3 -m http.server 8000
# then open http://localhost:8000/kuro.html

# or, if you have Node.js
npx serve .
```

## Editing the app

Everything lives in one file:
- `<style>` block — all CSS (colors, layout, animations)
- `<script>` block — all app logic (notes, tasks, goals, storage, routing)

Search for `KEYS` near the top of the script for the `localStorage` key names, and `state` for how data is structured in memory.

## About your data

- Everything you write — notes, tasks, goals — is saved to your browser's `localStorage`, scoped to wherever you're opening the file from (a specific `file://` path, or `http://localhost:PORT`).
- **This means your data is local to one browser on one device**, and tied to how you're opening the file. If you open it via Live Server on port 5500 one day and directly as a `file://` the next, the browser treats those as different storage buckets — you'll want to stick with one method consistently.
- There is no account, sync, or cloud backup. Clearing your browser's site data for that origin will erase your journal.
- If you want to back up your entries, the simplest approach is to open your browser's DevTools console on the page and run:
  ```js
  copy(JSON.stringify({
    notes: JSON.parse(localStorage.getItem('kuro_notes') || '[]'),
    tasks: JSON.parse(localStorage.getItem('kuro_tasks') || '[]'),
    goals: JSON.parse(localStorage.getItem('kuro_goals') || '[]')
  }, null, 2))
  ```
  This copies all your data to your clipboard as JSON, which you can paste into a text file and save.

## Keyboard shortcuts

- `/` — open search
- `Esc` — close any open modal, search, or note detail view

Build yourself every single day.
