# HD Image Generator — Upscale & Enhance Photos

Turn ordinary photos into crisp, high-definition images — **100% in your browser**. No uploads, no sign-up, no server: your image never leaves your device.

**▶ Live on Asif SaaS Studio:** open the tools catalogue and choose *HD Image Generator* (slug `hd-image-generator`).

## What it does
1. **Upscale** — 1× Enhance / 2× HD / 3× / 4× Ultra, using progressive high-quality resampling (in ≤1.5× steps).
2. **Enhance** — gentle denoise (35% gaussian blend), per-pixel brightness / contrast / saturation correction, and 3×3 convolution sharpening.
3. **Download** — PNG (lossless), JPEG (quality 60–100) or WebP, saved as `<name>-HD.<ext>`.

Output is capped at 8000 px per side and 40 megapixels for browser-memory safety, with an on-screen note whenever a cap applies. Inputs are validated in plain language: supported types are PNG, JPEG, WebP, BMP and GIF (first frame), up to 25 MB; SVG, empty and corrupt files get their own explanations.

> **Honest scope:** this is smart enhancement, not AI super-resolution — it cannot invent detail that was never captured. True AI upscaling needs a cloud AI backend; the documentation (Section 11) lays out that deployment plan openly.

## Use
Open `index.html` in any modern browser — or from this repo via any static host. No build step, no dependencies.

- Single file, **22.4 KB**, all CSS/JavaScript inline
- No localStorage, no service workers, no browser permissions, no parent-window access — safe in a sandboxed iframe
- Responsive layout in the Asif SaaS Studio emerald + lime branding

## Testing
18/18 automated tests passed (Node.js, executed against the shipped file's own image-maths core): pixel adjustments, sharpen/denoise kernels, size caps and all validation rules. Full report: `hd-image-generator-test-report.md`. Complete documentation: `docs/hd-image-generator-docs.pdf`.

Created by Dr. Asif Ahmad · Asif SaaS Studio · v1.0
