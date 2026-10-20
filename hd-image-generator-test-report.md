# HD Image Generator v1.0 — Test Report & Product Listing

**File:** `index.html` (22.4 KB — limit 150 KB) · single file, all CSS/JS inline, zero external assets, zero network calls, no localStorage, no service workers, no permissions, no parent-window access. Safe for the sandboxed Wix iframe.

## What it does
The user uploads a photo; the app enlarges it with progressive high-quality resampling (1× enhance / 2× HD / 3× / 4× Ultra), applies gentle denoise (35% gaussian blend), per-pixel brightness/contrast/saturation correction and a 3×3 sharpening convolution, then returns a downloadable PNG/JPEG/WebP. Output is capped at 8000 px per side and 40 megapixels for browser-memory safety (a visible note appears when the cap applies).

**Honest scope:** this is smart enhancement, not AI super-resolution. It cannot invent detail that was never captured — true AI upscaling requires a cloud AI backend with API keys, which the sandbox rules exclude. The page itself says this plainly.

## Product listing (for the Asif SaaS Studio CMS — `SaasProducts`)
- **Name:** HD Image Generator — Upscale & Enhance Photos
- **Slug:** `hd-image-generator`
- **Category:** Design
- **Version:** 1.0
- **Summary:** Turn ordinary photos into crisp HD images in your browser: 1×–4× high-quality upscaling with sharpening, denoise and colour correction. Download as PNG, JPEG or WebP. Your image never leaves your device.
- **appHtml:** upload `index.html` (this file)
- **Demo:** Yes · **Published:** Yes

## Automated tests — 18/18 passed (Node, run against the shipped file's own code)
1. Neutral settings (100/100/100) leave pixels unchanged
2. Brightness +50 raises pixel values
3. Saturation 0 produces true greyscale (r=g=b)
4. Contrast 150 darkens dark tones; contrast 50 lifts them
5. Identity convolution kernel returns the image unchanged
6. Sharpening a perfectly flat image changes nothing (no artefacts invented)
7. Gaussian denoise kernel on a flat image changes nothing
8. Sharpening widens a real edge (50→0 on the dark side, 200→255 on the bright side)
9. 2× size calculation exact (1000×800 → 2000×1600, uncapped)
10. Pixel cap engages correctly (6000×6000 @4× → 6324×6324, 40 MP)
11. Side cap engages correctly (5000×1000 @4× → 8000×1600)
12. Validation: no file → error; valid PNG → passes; SVG → rejected with explanation; non-image → rejected; 26 MB → rejected; empty file → rejected
13. Full inline script passes a JavaScript syntax check; file size verified at 22.4 KB

## Manual testing checklist
- [ ] Open `index.html` in Chrome/Edge — loads cleanly, no console errors
- [ ] Upload a small JPEG → preview, filename, dimensions and size appear
- [ ] Drop a `.txt` file on the drop zone → clear "not a supported image" error
- [ ] Try an SVG → "SVG files are not supported" message
- [ ] Generate at 2× with defaults → result preview shows doubled dimensions
- [ ] Compare Sharpen 0 vs 100 on a soft photo → visible crispness difference
- [ ] Download each format (PNG / JPEG / WebP) → file saves as `<name>-HD.<ext>`
- [ ] Upload a very large photo at 4× → capped-size note appears, app stays responsive
- [ ] Narrow the window to ~380 px → layout stacks, all controls reachable
- [ ] After CMS upload, open `app.html?slug=hd-image-generator` on the live site → app loads and processes inside the iframe

## Upload steps (Wix)
1. Wix dashboard → CMS → **SaasProducts** → add item with the listing fields above.
2. Paste the full contents of `index.html` into the **appHtml** field (or use the same upload route used for ColourShift).
3. Set **Published = Yes**, save, then open the live app page to verify.

*Note: GIFs are processed as their first frame; EXIF rotation is honoured by modern browsers when the photo is drawn.*
