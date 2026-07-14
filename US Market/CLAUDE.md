# CLAUDE.md — US Market

US-equity research workspace. Static dashboard + research pages (formerly "Macro Trader HTML").
Bilingual only where a page is explicitly the 中文 twin; otherwise English.

## Source material lives in `Market Research/` — look there FIRST

**Before doing any market analysis or building/updating a research page, check
`Market Research/` for the original source works and base the analysis on them.**

That folder holds the primary inputs — broker reports, data exports, filings, transcripts,
and research notes. Treat what's in it as **ground truth**: derive numbers, quotes, and
claims from those files rather than inventing figures or relying on memory. When a page makes
a factual claim, it should be traceable to a file in `Market Research/` (or to `live_data.js`
for the refreshable market numbers). Cite the source file/date in the page where practical.

**All future market research materials go into `Market Research/`** — see its `README.md`
for naming and layout conventions. Finished HTML pages still go under `pages/<type>/`; only the
raw/source works go in `Market Research/`.

> Migration note: two source PDFs still sit in `assets/docs/`
> (`Strategic_Market_Rotation.pdf`, `The_2026_Market_Paradigm_Shift.pdf`) — they're the
> inputs behind the two `pages/recaps/` weekly notes and are linked from those pages via
> `../../assets/docs/`. New source material should not follow them there; it belongs in
> `Market Research/`. Moving the existing two would require updating those page links first.

## Folder map (quick)

- `index.html` — hub, cards grouped by type (one section per `pages/` subfolder).
- `pages/<type>/` — finished pages: briefings · valuation · value-line · recaps · technical · etf · tools · frameworks.
- `Market Research/` — **original source works to analyze (inputs).**
- `assets/js/live_data.js` — single source of truth for refreshable market numbers; 5 pages consume it (its header lists which).
- `macro-trader-UPDATE_GUIDE.md` — agent contract: refresh the technical page by editing only `pages/technical/macro-trader-data.json`.
- `README.md` — fuller folder map, naming conventions, refresh steps.

## When adding a page

1. Build it from source material in `Market Research/`.
2. Drop the file in the matching `pages/<type>/` subfolder (kebab-case, ISO dates).
3. Add its card to `index.html` under the section for that type, or it's orphaned.
4. Content pages sit two levels deep — reference assets as `../../assets/...`, link home as `../../index.html`.

## How to generate a report page — style & format

Every page is a **self-contained single-file HTML** report: all CSS in one `<style>` block,
all JS in one `<script>` block, no build step, opens in a browser. Match the existing pages —
don't invent a new look. Copy the skeleton from `pages/valuation/sp500-valuation-report.html`
(the canonical example) and adapt.

### House style (the default for briefings, valuation, technical, ETF, tools)

- **Font:** Inter — `<link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800&display=swap" rel="stylesheet">`. Body `font-size:14px`, `line-height:1.6`.
- **Charts:** Chart.js 4.4.1 from **cdnjs** — `<script src="https://cdnjs.cloudflare.com/ajax/libs/Chart.js/4.4.1/chart.umd.min.js"></script>`. No other libraries.
- **Palette — define these `:root` vars verbatim** (light theme, cool grays + navy):
  ```css
  :root{
    --bg:#F5F6F7; --bg2:#FFFFFF; --bg3:#F0F1F3;          /* page / surface / sunken */
    --text:#1E1E1E; --text2:#5B5B5B; --text3:#8A8A8A;    /* ink / muted / faint  (--muted is an alias of --text2) */
    --border:#E5E5E5; --border2:#D5D5D5;
    --navy:#1B3A5C; --navy-dark:#122A45;                 /* headers, brand */
    --green:#00936C; --red:#C72E0B; --amber:#D8A000;     /* semantic */
    --blue:#2A6CB8; --purple:#7B5EA7; --teal:#007A90; --orange:#E07B2D;  /* accents */
  }
  ```
- **Direction convention: US markets — GREEN = up, RED = down.** (Opposite of `../China Market/`, which is red-up. Never mix them.)

### Page skeleton (in body order)

```
.header                      navy band
  .header-top
    .header-badge            e.g. "Investment Committee Report"
    <h1> …<span class="accent">— subtitle</span></h1>
    .header-meta             "As of <span data-live="asOfLong">…</span> · <team>"
  .header-actions            <button class="btn-ghost" onclick="window.print()">Print / PDF</button>
.kpi-strip                   row of .kpi cards
  .kpi > .kpi-label / .kpi-value[.green|.red|.navy] / .kpi-sub
.tabs[role=tablist]          .tab buttons, first is .active, each has data-tab="id"
.main
  .section[.active]#id       one per tab; only .active is shown
    .section-heading + .section-sub    (sub is a one-line framing sentence)
    .card / .grid-2 / .kpi / table / .chart-wrap > <canvas> / .insight callout / .pill badges / .bullet lists
<footer>                     source + as-of date
```

### Tab switching JS (standard — copy as-is)

```js
const tabs = document.querySelectorAll('.tab');
const sections = document.querySelectorAll('.section');
tabs.forEach(t => t.addEventListener('click', () => {
  const id = t.dataset.tab;
  tabs.forEach(x => x.classList.remove('active'));
  sections.forEach(s => s.classList.remove('active'));
  t.classList.add('active');
  document.getElementById(id).classList.add('active');
  window.scrollTo({ top: 0, behavior: 'smooth' });
}));
```

### Wiring refreshable numbers

Any market number that goes stale should be a `<span data-live="key">fallback</span>` bound to
`assets/js/live_data.js` (add `<script src="../../assets/js/live_data.js"></script>` before
`</body>`). Use an existing key if one fits; only hard-code numbers that never refresh.
See `macro-trader-UPDATE_GUIDE.md` for the technical-setup page's separate JSON-driven pattern.

### Recaps use a different look on purpose

Dated one-off notes in `pages/recaps/` use an **editorial variant** — serif (`Newsreader` +
`IBM Plex Sans`), warm cream `--bg:#f3efe8`, `--risk-on`/`--risk-off` accents. Use it for
narrative recap notes; use the house style above for everything else. Match whichever the
sibling files in the target `pages/<type>/` folder already use.

### Rules

- Base every number and claim on `Market Research/` (or `live_data.js`); make it traceable.
- Explicit date range on the page (header meta + footer). ISO dates.
- Self-contained, responsive, no external calls beyond the two CDNs above.
- After adding the page: card in `index.html`, verify the `../../` asset/home links resolve.
