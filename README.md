# Analecta

A D3.js star map for your research library. Each source is a node. Clusters group by domain. Connections map intellectual overlap. Click any node to read the thesis.

**[Live example → psychoid.fm/analecta](https://psychoid.fm/analecta)**

---

## What it is

Analecta turns a reading list into a navigable constellation. It is not a citation manager or a knowledge graph in the academic sense — it is a *thinking tool*. It is built for orientation, not storage. The spatial layout makes the shape of your intellectual territory visible at a glance.

The key layer is the **thesis**: a 2–3 sentence interpretive compression of each work. Not an abstract. Not a summary. A distillation of why the paper matters *to you*, what it changes, what it opens up. Writing these forces you to actually have a position on what you read.

## Setup

No build step. No dependencies to install. It is one HTML file.

### Option A — In-browser editor (no code required)

1. Fork this repo and enable GitHub Pages, or download `index.html` and open it in a browser
2. Click **EDIT** (bottom right) to open the editor panel
3. Add your papers, domains, and connections through the form — no code editing needed
4. Your map auto-saves to your browser's local storage
5. Use **Data → Export JSON** to download a backup file you can reload anytime

### Option B — Edit the code directly

1. Fork or download this repo
2. Open `index.html` in a text editor
3. Edit the `CLUSTERS` object with your domains
4. Add your own papers to the `entries` array (the comments will guide you)
5. Add connections in the `links` array
6. Update the header and home link to match your site
7. Host anywhere — GitHub Pages, Netlify, cPanel, or open it locally in a browser

## The editor

The **EDIT** button opens a panel with three tabs:

- **Entries** — add, edit, or delete papers. Set the title, authors, date, domain, thesis, URL, and convergence flag. Tick checkboxes to draw connections to other entries.
- **Domains** — add or edit research clusters. Choose a name, key, and color.
- **Data** — export your map as a JSON file, import a previous export, or reset to the template.

All changes auto-save to `localStorage`. Your map persists across page refreshes without any account or server. Export regularly as a backup.

---

## The entry format

```javascript
{
  id: 1,                     // unique integer, used by the links array
  num: "001",                // display label shown under the node
  cluster: "your_cluster",   // must match a key in CLUSTERS
  title: "Paper Title",
  authors: "Author, Coauthor — Institution",
  date: "Month Day",         // freeform string
  thesis: "2–3 sentences. Interpretive, not descriptive. What does this change?",
  convergence: false,        // true = glowing halo ring; use for your most significant entries
  url: "https://..."         // or null to hide the source link
}
```

## Writing the thesis

This is the hardest and most valuable part. The thesis is not a summary — it is a compression of *significance*. What does this paper prove, disrupt, or open? What would a smart reader miss if they skipped it? Write in present tense, active voice, 2–3 sentences maximum.

**Timing matters:** write the thesis during or immediately after reading, while the encounter is still warm. You can summarize later. You cannot interpret later.

**Avoid:** *"This paper examines the relationship between X and Y, showing that Z may play a role in W."*

**Aim for:** *"Driven matter spontaneously self-organizes into structures that dissipate energy more efficiently — making life a thermodynamic inevitability rather than accident. The physics reason life had to happen."*

The difference: the first describes. The second stakes a claim.

## Customizing clusters

Use the **Domains** tab in the editor, or edit the `CLUSTERS` object directly in the code:

```javascript
const CLUSTERS = {
  your_key: { name: "Full Display Name", color: "#hexcolor", short: "ABBREV" },
};
```

Then add that cluster's position in `getLayout()` under all three layout modes (desktop, landscape phone, portrait phone). Copy the pattern already there.

## Force tuning

The `simForces()` function controls how nodes physically arrange themselves:

| Parameter | Default | Effect |
|-----------|---------|--------|
| `clusterStr` | 0.30 | Gravity toward cluster center. Higher = tighter groups. |
| `chargeStr` | -160 | Repulsion between nodes. More negative = more spread. |
| `collideR` | 22 | Collision radius. Increase if nodes overlap badly. |
| `linkDist` | 75 | Preferred length of connection lines. |

For small libraries (under 30 entries), try `clusterStr: 0.45`, `chargeStr: -80`, `collideR: 14`.

## Convergence

Mark your most important entries with `convergence: true`. They render with a glowing outer ring and the CONVERGENCE button filters to show only them, pulling them toward the center. Use sparingly — 10–20% of your library at most. It should feel like a highlight, not a default.

## Deploying

The file is self-contained — one HTML file with no external assets other than fonts (Google Fonts CDN) and D3 (Cloudflare CDN). To deploy:

- **GitHub Pages:** Push to a repo, enable Pages in settings
- **Netlify:** Drop the folder into the Netlify dashboard
- **cPanel / any host:** Upload `index.html` to your public directory
- **Locally:** Just open `index.html` in a browser — it works without a server

---

Built by [Lueda Alia](https://iamlueda.com). The live instance lives at [psychoid.fm/analecta](https://psychoid.fm/analecta).
