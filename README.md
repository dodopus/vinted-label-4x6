# Vinted Label Cropper

A tiny static web app that crops a Vinted **InPost A4** shipping sheet down to
just the **4×6 label** and rotates it upright — ready to print.

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

## Tuning

Everything is in the `<script>` block of `index.html`:

- `BOX` — the label's position on the A4 template, in PDF points. Mapped once;
  the Vinted template is fixed so it never needs changing.
- `PAD` — margin (pt) around the label so nothing clips. Bump it if a future
  label ever gets cut off.
- `ROTATE` — `270` stands the sideways label upright (verified).
