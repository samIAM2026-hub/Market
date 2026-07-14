# US Market

Static market dashboard and research pages for the US-equity research workspace
(formerly the "Macro Trader HTML" site).

## Folder Map

- `index.html` — main hub for the site (the only HTML at the root).
- `Market Research/` — **original source works to analyze (inputs)** — broker reports, data
  exports, filings, notes. Pages are built *from* this; see its `README.md`. All new research
  material goes here.
- `pages/` — all content pages, grouped by type:
  - `pages/briefings/` — daily / earnings / strategic-outlook market reads.
  - `pages/value-line/` — Value Line Summary & Index and Selection & Opinion explorers (incl. 中文 twin).
  - `pages/valuation/` — S&P 500 valuation, index reference, AI value-chain.
  - `pages/frameworks/` — educational frameworks (DCA, market-monitoring synthesis).
  - `pages/recaps/` — dated one-off notes (daily/weekly recaps, comparatives).
  - `pages/technical/` — Macro Trader technical setup + its `macro-trader-data.json`.
  - `pages/etf/` — ETF research (Canadian ETF report).
  - `pages/tools/` — utilities (live-data viewer).
- `assets/js/live_data.js` — shared refreshable market data. Five pages consume it; the file's
  own header comment lists exactly which, and is the thing to keep in sync when that changes.
- `assets/img/`, `assets/docs/` — image decks and PDF deliverables referenced by pages.
- `macro-trader-UPDATE_GUIDE.md` — agent contract for refreshing the technical setup page by
  editing only `pages/technical/macro-trader-data.json`. Read it before touching that page.
- `_archive/backups/` — local, gitignored backup files. Not part of the site.

## Conventions

- **Filenames**: kebab-case with ISO dates — single dates as `YYYY-MM-DD`
  (e.g. `us-market-recap-2026-06-12.html`), ranges as `YYYY-MM-DD-to-DD`
  (e.g. `strategic-outlook-2026-05-24-to-06-07.html`).
- **Relative paths**: content pages sit two levels below the root, so they reference
  shared assets as `../../assets/...` and link back to the hub as `../../index.html`.

## Updating Market Data

1. Edit `assets/js/live_data.js`.
2. Open `pages/tools/live-data-viewer.html` to review the complete data snapshot.
3. Open `pages/briefings/daily-briefing.html` and the main hub to confirm the site still loads cleanly.

## GitHub Pages

Arranged for simple GitHub Pages hosting. Keep `index.html` at the folder root and all
content under the typed `pages/` subfolders. When adding a page, drop it in the matching
subfolder and add its card to `index.html`.

`index.html` groups its cards **by type**, one section per `pages/` subfolder, in this order:
Briefings · Valuation · Value Line · Recaps · Technical · ETF · Frameworks · Tools. A new page
therefore has exactly one correct section — the one named after its folder. Adding the file
without adding the card leaves it orphaned and unreachable from the hub.
