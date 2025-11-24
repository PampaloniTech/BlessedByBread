# Performance measurement guide

Use these steps to capture before/after metrics locally so you can compare improvements.

## 1) Serve the site locally
- From the repo root, start a lightweight server:
  - **Python**: `python -m http.server 8000`
  - or **Node** (if preferred): `npx serve . -l 8000`
- Visit `http://localhost:8000` to verify the site is reachable.

## 2) Run Lighthouse for lab metrics
- Install Lighthouse if you don't already have it (`npm install -g lighthouse`, or run from Chrome DevTools > Lighthouse).
- From the repo root while the server is running:
  - **Mobile profile:** `lighthouse http://localhost:8000 --preset=mobile --only-categories=performance --output=json --output-path=before-mobile.json`
  - **Desktop profile:** `lighthouse http://localhost:8000 --preset=desktop --only-categories=performance --output=json --output-path=before-desktop.json`
- After applying changes, repeat the commands with filenames `after-mobile.json` and `after-desktop.json`.
- Compare the scores and key metrics (First Contentful Paint, Speed Index, Total Blocking Time) between the before/after JSON outputs.

## 3) Spot-check in Chrome DevTools
- Open DevTools > Performance and record a page load with throttling set to "Fast 3G" to visualize parse/paint times.
- Use the Network panel to confirm fonts load via preconnect and that images are served with their intrinsic dimensions (no layout shifts).

## 4) Optional external check
- If you prefer a third-party view, run a test on [WebPageTest](https://www.webpagetest.org/) with the site URL and keep the summary waterfall screenshots for before/after comparison.

Saving the four Lighthouse JSON files (`before/after` x `mobile/desktop`) in source control or your notes will give you a reproducible record of the performance gains.
