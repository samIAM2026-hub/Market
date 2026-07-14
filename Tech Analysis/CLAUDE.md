# CLAUDE.md — Tech Analysis

Technical / chart analysis for the Hobby project. Follow this routing when working here.

## Where things go

- **Incoming research papers / notes** (`.md`) → `Charts/md file/`. This includes any research paper, source write-up, or dated ChartList analysis (e.g. Dave Keller Market Misbehavior files) that comes in as raw material.
- **Final reports** (finished HTML analysis) → `Report/`.
- **Chart assets**, sorted by type: `.png` → `Charts/Image/`, `.json` → `Charts/json/`, `.md` → `Charts/md file/`.

Never create a separate `outputs/` folder.

## Flow

Research paper comes in → save the `.md` under `Charts/md file/` → build the analysis → save the final report as HTML in `Report/`. When a new report is added, also add a linking card to the root `index.html`.

## Report design & style

Reports are **self-contained single-file HTML** with a **light technical-dashboard** look (not the
dark finance style). All three reports in `Report/` share one `:root` token set — copy it so new
reports match:

```css
:root{
  --bg:#f4f6f9; --panel:#ffffff; --ink:#1a2230; --muted:#5d6b80;
  --line:#e3e8ef; --navy:#1f3a5f; --accent:#2563eb;
  --bull:#1f9d6b; --bull-bg:#e7f6ef;   /* uptrend / bullish */
  --bear:#d64545; --bear-bg:#fcecec;   /* downtrend / bearish */
  --caut:#d98a17; --caut-bg:#fdf3e2;   /* caution */
  --ext:#0d8f9e;  --ext-bg:#d8f1f4;    /* extended / overbought-oversold */
  --neut:#6b7280; --neut-bg:#eef1f5;   /* neutral */
  --font:-apple-system,BlinkMacSystemFont,"Segoe UI",Roboto,Helvetica,Arial,sans-serif;
}
```

- **US-market convention: green = up (`--bull`), red = down (`--bear`).** (Opposite of `../China Market/`.)
- Light page (`--bg`), white panels, navy headers, semantic trend chips. System font stack.

**Source of truth for the report format is the `stockcharts-technical-report` skill** — invoke it to
generate a report rather than hand-building; it produces this token set and layout. Keep new reports
visually consistent with the existing three in `Report/`.
