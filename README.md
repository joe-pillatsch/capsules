# Capsules — An Atlas of 151 Colors

Capsules is a single-page visual atlas of 151 capsules, each distilled to one
defining color — the hue of its top **dome** — and every one inscribed
**byte-perfect on Bitcoin** as an [Ordinal](https://docs.ordinals.com/). Specimens
are identified by number (№ 001–151), not by name.

The site presents the 151 colors three ways:

- **The Flipbook** — an animated hero that cycles through all 151 sprites.
- **The Spectrum** — all 151 dome colors as a single hue-sorted bar; click any
  stripe to inspect.
- **The Atlas** — a responsive grid of every specimen, with a lightbox detail
  view linking out to the live on-chain inscription.

## The file to edit: `index.html`

`index.html` is the whole app as **ordinary, readable source** — plain CSS in a
`<style>` block and plain JavaScript in `<script>` tags. Edit it in any text
editor. React + Babel and the web fonts load from CDNs; the JSX is transpiled in
the browser at load (no build step).

It needs two things alongside it:

- **`images/`** — the 151 sprite PNGs, loaded as `images/{n}.png`.
- **Network** — for the CDN scripts/fonts, and for specimen **#53** + the
  lightbox "view on-chain" links, which load from `ordinals.com`.

### Hosting / running

Built for normal HTTP hosting — drop the folder on **GitHub Pages** (or any
static host) and it works. `index.html` is the default document, so the site
root serves it.

To preview locally you can also just **double-click `index.html`** — because all
the code is inline, it runs from `file://` too (only #53 and the CDN/font
requests need the network). Or serve it:

```bash
cd "Pokéball Color Atlas"
python3 -m http.server 8000   # then open http://localhost:8000/
```

### Changing how it looks

Near the top of the inline app script is a plain `SETTINGS` object — edit the
values directly:

```js
const SETTINGS = {
  theme: "dark",        // "dark" | "light"
  flipbook: "flicker",  // "flicker" | "fade" | "morph" | "filmstrip"
  tempo: 1,             // 1–12 (1 = slowest hero cycling)
  order: "dex",         // "dex" | "spectrum"
  labels: "name",       // "none" | "index" | "name" | "full" (cards show the number)
  tile: 132,            // grid tile size, 92–200 px
  heroScale: 440,       // hero sprite size, 180–440 px
  accent: "#f5b13d",    // #e8513a red · #36d6c3 teal · #8b7cf6 violet · #f5b13d orange
  glow: true,
  scan: true,           // CRT scanline overlay
};
```

## How the colors work

Each sprite is a capsule whose **top dome** is recolored while the lower half,
band, and button stay structural white/black/grey. The authoritative dome color
for every capsule (plus its full Bitcoin inscription id) is baked into
`window.DOME_COLORS` / `window.INSCRIPTIONS` in the inline scripts — keyed by
number 1..151 — so the atlas renders instantly without sampling pixels at
runtime.

Collection facts: **151** specimens, **144** unique hues, inscriptions
**#194,259–#195,670** on Bitcoin via Ordinals.

## Project layout

```
Pokéball Color Atlas/
├── index.html      # the app — plain editable source (THIS is what you edit/host)
├── images/         # 1.png..151.png sprites (loaded by index.html)
└── screens/        # screenshots
```
