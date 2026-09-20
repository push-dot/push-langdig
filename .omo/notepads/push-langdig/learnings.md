
## 2026-09-19 landing rebuild
- Files: index.html (HTMX 2.0.6 + @tailwindcss/browser 4.1.12 CDN, inline @theme tokens), fragments/download-ok.html, assets/{cards.csv,starter-guide.md,push-langdig-starter.zip}, DESIGN.md, README.md.
- Download UX: `hx-get` fragment swap into `#download-status` (aria-live) + `hx-on::before-request` programmatic `a[download]` click; no-JS fallback is the native `download` attr.
- Mobile nav: `details/summary` (no JS). Anchors: #features #how #privacy #download.
- Smoke: `python3 -m http.server 4173`; curl 200 on /, fragment, zip.
- Repo surprise: remote push-dot/push-langdig already had develop+main history; committed `3a89a8e` on develop, PR #3 squash-merged into main, develop kept.
- Debt: CDN Tailwind JIT (not compiled), CDN fonts, no visual regression suite.
