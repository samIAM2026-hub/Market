# Market Research — source materials

**This folder holds original research works — the primary source material that the
dashboard pages are built from.** Inputs live here; the published HTML pages under
`../pages/` are the outputs.

Put here anything that is *evidence to analyze*, not a finished page:

- Broker / sell-side research reports (PDF)
- Data exports and downloads (CSV, XLSX, JSON)
- Article clippings, transcripts, filings, screenshots of terminals
- Your own research notes, theses, and working drafts (MD / TXT)
- Anything a page cites as its source of numbers or claims

## Conventions

- **Name with a date + subject**, ISO first: `2026-07-10-factset-earnings-insight.pdf`,
  `2026-06-us-hy-oas-fred-export.csv`. This keeps the newest material sortable and makes
  it obvious which vintage a page was built from.
- **Group by topic once a subject grows** — e.g. `earnings/`, `valuation/`, `rates-credit/`,
  `fed/`. Keep it flat until a folder earns its own subfolder.
- **Don't delete stale source material** — a page's numbers should always be traceable back
  to the exact input they came from. Add new vintages alongside old ones.
- **Never commit private/account data** — brokerage statements, positions, account numbers,
  API keys. This is a public GitHub Pages repo. Source material must be research, not records.

## Not here

- Finished pages → `../pages/<type>/`
- Live/refreshable numbers wired into pages → `../assets/js/live_data.js`
- Image decks and PDFs a page links to and *displays* → `../assets/`
