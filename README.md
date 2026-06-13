# Capsules

**151 capsules. 151 colors. 151 Inscriptions on Bitcoin.**

An art project representing the original 151 — each capsule distilled to a single defining hue and inscribed *byte-perfect* on Bitcoin via [Ordinals](https://docs.ordinals.com/). Specimens are identified by number (№ 001–151), not by name.

**[→ capsules.joepillatsch.com](https://capsules.joepillatsch.com)**

---

## The collection

| | |
|---|---|
| Specimens | 151 |
| Unique hues | 144 |
| Inscriptions | [#194,259 – #195,670](https://ordinals.com) · Bitcoin |

Three views: **The Flipbook** cycles all 151 sprites in an animated hero. **The Spectrum** shows all 151 dome colors sorted by hue — click any stripe to inspect. **The Atlas** is a full grid with a lightbox linking to each live on-chain inscription.

---

## Editing

The entire app is one plain file: `index.html`. Open it in any text editor.

To change how it looks, edit the `SETTINGS` object near the top of the script:

```js
const SETTINGS = {
  theme: "dark",        // "dark" | "light"
  flipbook: "flicker",  // "flicker" | "fade" | "morph" | "filmstrip"
  tempo: 1,             // 1–12  (1 = slowest)
  order: "dex",         // "dex" | "spectrum"
  labels: "name",       // "none" | "index" | "name" | "full"
  tile: 132,            // tile size in px  (92–200)
  heroScale: 440,       // hero size in px  (180–440)
  accent: "#f5b13d",    // brand color
  glow: true,
  scan: true,
};
```

No build step. React + Babel load from CDN; JSX is transpiled in the browser.

---

## Running locally

Double-click `index.html` — it runs from `file://`. Or serve it:

```bash
python3 -m http.server 8000
```
