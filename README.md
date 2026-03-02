# The Wavelet Transform — A Visual Guide

An interactive, animated guide to understanding wavelet transforms, built entirely with vanilla HTML Canvas and JavaScript. No dependencies, no build step — just open `index.html`.

**[→ View the Live Guide](https://brendanjameslynskey.github.io/WaveletTransformGuide/)**

---

## What's Inside

The guide walks through wavelet theory in seven chapters, each with real-time animated visualisations you can interact with.

### 1 · The Core Intuition
Drag sliders to scale and translate a Morlet wavelet across a signal. See how the wavelet acts as a local probe — short wavelets catch fast oscillations, stretched wavelets capture the slow trend.

### 2 · Fourier vs Wavelet
A chirp signal (frequency sweeping from low to high) is analysed two ways side-by-side. The Fourier power spectrum shows which frequencies exist but loses all timing. The wavelet scalogram reveals exactly when each frequency appears.

### 3 · Mother Wavelets
Switch between Morlet, Haar, Mexican Hat, and Daubechies-4 to see how wavelet shape determines what the transform is sensitive to. Each is shown at multiple scales with an animated scanning wavelet.

### 4 · Continuous Wavelet Transform (CWT)
Watch the CWT build a scalogram row-by-row. A wavelet slides across a composite signal at each scale, and the resulting correlation coefficients fill in a time–scale heatmap in real time. Adjustable animation speed.

### 5 · Discrete Wavelet Transform (DWT)
An animated filter bank decomposition splits a signal into approximation and detail coefficients at each level using the Haar wavelet. The cascade of low-pass / high-pass filtering and downsampling is shown step by step.

### 6 · Multiresolution Analysis
Choose from three signal types (composite, step+sine, noisy sine) and see them decomposed into four detail levels. Demonstrates how wavelets separate structure at different scales — and how the original can be perfectly reconstructed.

### 7 · Denoising Application
Add noise to a clean signal, then apply wavelet thresholding to recover it. Interactive controls for noise level and threshold, with an animated reconstruction sweep.

---

## Deploy to GitHub Pages

This is a single-file project — `index.html` contains everything.

**Option A — Repository root:**

```bash
git init wavelet-guide && cd wavelet-guide
# copy index.html into this directory
git add index.html
git commit -m "Initial commit"
git remote add origin git@github.com:yourusername/wavelet-guide.git
git push -u origin main
```

Then go to **Settings → Pages → Source → Deploy from a branch → `main` / `/ (root)`**.

**Option B — `docs/` folder** (if you want to keep other files at the root):

```bash
mkdir docs
cp index.html docs/
git add docs/
git commit -m "Add guide to docs/"
git push
```

Set Pages source to `main` / `/docs`.

Your guide will be live at `https://yourusername.github.io/wavelet-guide/`.

---

## Technical Details

- **Zero dependencies.** No npm, no bundler, no external JS libraries. All rendering uses the HTML Canvas API.
- **All maths is computed in real-time.** The CWT scalograms, DFT spectra, and Haar DWT decompositions are calculated on the fly in the browser — no pre-baked data.
- **Responsive.** Canvases scale with DPR for sharp rendering on Retina/HiDPI displays.
- **Accessible colours.** The dark theme uses high-contrast accent colours against a near-black background, with sufficient luminance ratios for readability.

### What's computed where

| Visualisation | Algorithm | Notes |
|---|---|---|
| CWT scalogram | Morlet inner product at 40–60 scales | Brute-force O(N²) per scale, fast enough for N ≤ 512 |
| Fourier spectrum | Naive DFT | Sufficient for the 512-sample demo signal |
| DWT decomposition | Haar filter bank | Iterative split → downsample at 4 levels |
| Denoising | 3-level Haar DWT + soft thresholding | Reconstruct via inverse Haar |

---

## Customisation

Everything lives in one file, so edits are straightforward.

**Change the colour scheme** — modify the CSS custom properties at the top of `<style>`:

```css
:root {
  --accent:  #4fc3f7;   /* primary blue    */
  --accent2: #ab47bc;   /* purple           */
  --accent3: #66bb6a;   /* green            */
  --accent4: #ffa726;   /* orange           */
}
```

**Swap signals** — each chapter's IIFE generates its own signal array. Search for the `signal(t)` or `sig[i]` definitions and replace with your own functions.

**Add a chapter** — copy an existing `<section>` block, give it a new `id`, add a matching `<a>` in the table of contents, and write a new canvas + drawing IIFE at the bottom of the script.

---

## License

MIT — use it however you like. Attribution appreciated but not required.
