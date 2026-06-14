# Vinted Label Cropper

A tiny static web app that crops a Vinted A4 shipping sheet down to just the
**4×6 label** and rotates it upright — ready to print.

- **Carrier-agnostic.** Works across formats (InPost, Evri, …) by auto-detecting
  the label rather than hardcoding one carrier's position — no per-carrier table.
- **100% in-browser.** Your label PDF never leaves your device (no server, no upload).
- **Vector-perfect.** It rewrites the PDF page box and rotation rather than
  rasterizing, so barcodes and text stay razor-sharp at any size.
- **Batch.** Drop multiple PDFs at once; each downloads as `<name>_label.pdf`.

## Use it

Open `index.html` in any browser, or visit the deployed site, then drag in
(or click to choose) your Vinted PDFs.

## Deploy to GitHub Pages

1. Put these files in a repo (the `index.html` + `pdf-lib.min.js` must sit
   together — e.g. both in the repo root, or both in a `/docs` folder).
2. Repo **Settings → Pages → Build and deployment**.
3. Source: **Deploy from a branch**, branch `main`, folder `/ (root)`
   (or `/docs` if you put them there).
4. Save. Your site appears at `https://<user>.github.io/<repo>/` in a minute or two.

No build step — it's plain static files.

## How detection works

Every carrier draws the label as a form XObject sized ~4×6 (100×150mm) on an
otherwise A4 sheet. `findLabelBox()` in `index.html` walks the page content
stream, tracks the CTM through `q`/`Q` + `cm`, and computes the page-space
rectangle of each placed XObject. `labelScore()` keeps the one whose dimensions
match a 4×6 label and rejects the A4-sized background. The app then crops to that
box and rotates 270° only if the box is landscape.

## Tuning

In the `<script>` block of `index.html`:

- `PAD` — margin (pt) around the label so the border stroke never clips. Bump it
  if a future label ever gets cut off.
- `labelScore()` — the size window that decides what counts as a 4×6 label. Widen
  the bounds if a new carrier uses a slightly different label size.
