# CLAUDE.md

Guidance for working in this repo. See [README.md](README.md) for the
product-level overview.

## What this is

Capsules is an **atlas of 151 capsules distilled to one dome color each**, every
one inscribed on Bitcoin via Ordinals. Specimens are identified by **number**
(№ 001–151) — there are intentionally **no creature names** anywhere in the UI.

The app is **`index.html`** — a single, plain, hand-editable HTML file: CSS in a
`<style>` block, plain JS in `<script>` tags, and the app itself in one
`<script type="text/babel">` (JSX transpiled in the browser). React + Babel and
fonts come from CDNs. **No build step.** This is the only source of truth — there
is no separate bundle to keep in sync.

## Editing `index.html`

It's ordinary source — just use Edit/Write. The structure, top to bottom:

1. `<head>`: meta, `<title>`, Google Fonts `<link>`s, one `<style>` block with
   all the app CSS (CSS custom properties — `--accent`, `--bg`, etc.; theme
   switched via `data-theme` on `<html>`).
2. `<div id="root">`.
3. CDN `<script src>`: React 18.3.1, ReactDOM 18.3.1, `@babel/standalone`.
4. Two plain `<script>` blocks that attach globals to `window`:
   - `extractDomeColor`, `rgbToHex`, `colorSortKey`, `contrastInk` (color utils)
   - `DOME_COLORS`, `INSCRIPTIONS`, `COLLECTION`, `inscriptionUrl`,
     `inscriptionContent`, `shortId` (inscription data + helpers)
5. One `<script type="text/babel">`: the React app (components + `SETTINGS` +
   `ReactDOM.createRoot(...).render(<App/>)`).

Because everything is inline, the page runs from `file://` as well as over HTTP —
keep it that way (don't reintroduce cross-file `src` fetches for the app code;
Babel fetching an external `.jsx` is exactly what breaks `file://`).

## Numbers, not names

Specimens are referenced only by number. There is no `GEN1_NAMES` map — it was
removed along with every name in the UI (hero, spectrum tooltips, atlas tiles,
lightbox, image `alt` text). If you add UI that labels a specimen, use
`№ ${pad(n)}` — do **not** reintroduce creature names.

## `SETTINGS` (display config)

There is no runtime Tweaks panel — display config is the plain `SETTINGS` object
near the top of the babel script. Current values: `theme:"dark"`,
`flipbook:"flicker"`, `tempo:1`, `order:"dex"`, `labels:"name"`, `tile:132`,
`heroScale:440`, `accent:"#f5b13d"`, `glow:true`, `scan:true`. The app pushes
`accent`/`scan` onto the `--accent`/`--scan` CSS vars and reads the rest
directly. Valid ranges/options:

- `flipbook`: `flicker` · `fade` · `morph` · `filmstrip`
- `tempo`: 1–12 (1 = slowest hero cycling)
- `order`: `dex` · `spectrum` · `labels`: `none` · `index` · `name` · `full`
  (cards show the number; `full` adds the hex)
- `tile`: 92–200 px · `heroScale`: 180–440 px
- `accent`: `#e8513a` red · `#36d6c3` teal · `#8b7cf6` violet · `#f5b13d` orange
- `theme`: `dark` · `light` · `glow`/`scan`: booleans

## Runtime facts & gotchas

- **Indexing is 1..151**; numbers zero-pad to 3 digits via `pad(n)` for the
  `№ 001` labels.
- **Sprites are external.** Art resolves as `window.SPRITES?.[n] || "images/"+n+".png"`.
  `window.SPRITES` is not defined in this context, so every sprite loads from
  `images/{n}.png` — **`index.html` depends on the `images/` folder next to it.**
  Don't delete it.
- Dome colors + inscription ids are **baked into the inline scripts** —
  authoritative, no runtime pixel sampling. `extractDomeColor` is kept for
  regenerating that data, not used on the render path.
- **Verify visual changes** by serving the folder and loading `/` (the project
  root's `.claude/launch.json` has an `ordemon` config:
  `python3 -m http.server 4321 --directory "Pokéball Color Atlas"`). The only
  expected console warning is the in-browser Babel notice.
- **No git / version control** here (iCloud Drive). Edits and deletions are
  permanent — work on a copy if a change is risky.
