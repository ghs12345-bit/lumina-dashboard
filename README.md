# Lumina Metals — Dashboard

Interactive weekly dashboard for **Lumina Metals Corp.** (TSX: LMCU / WSE: LMU),
tracking the share price against the copper and silver prices that drive its
Nowa Sól and Mozów / Bytom Odrzański projects in Poland.

**Live page:** https://ghs12345-bit.github.io/lumina-dashboard/

## What it shows

**Stock data tab**

- Four series over the full available history on three axes, all in real units
  with no offsets or unit conversions applied:
  - **LMCU C$** (left) — TSX close, and **LMU zł** (same axis, comparable scale)
  - **Ag $/oz** (inner right) — LBMA silver
  - **Cu $/t** (outer right) — LME copper
- Summary cards for the latest copper, silver, TSX and WSE closes with
  day-over-day change (Chinese market convention: up is red, down is green).
- A range slider plus wheel zoom; axis labels collapse to one stamp per month
  in the full-history view and switch to day-level dates once zoomed in.

**Company profile tab**

- Project overview, mineral resource table, PEA highlights, share structure.
- Recent company news (relative dates, exact ISO date on hover) and sector news
  filtered to Polish / European copper, KGHM, copper-silver pricing and
  peer M&A.
- Analyst coverage, consensus target price with upside computed from the live
  close, bull / bear case, and a milestone timeline.

## Data sources

| Item | Source | Refresh |
|---|---|---|
| TSX close (LMCU) | stockanalysis.com | automated, weekly |
| WSE close (LMU) | stockanalysis.com | automated, weekly |
| LME copper, LBMA silver | project drive `Metal Prices/Metal Prices.xlsx` | **manual upload** — the last available row is reused when no new file is present |
| Company & sector news | Lumina newsroom, Yahoo Finance, MINING.COM, Stockhouse, The Northern Miner | automated, weekly |
| News release PDFs | project drive `News/` | manual |

## Update schedule

The pipeline runs **every Monday at 10:00** and rebuilds this page from the
sources above, then pushes the result to this repository.

## Known gaps

- **April 2026 is missing** for both tickers. stockanalysis.com only exposes the
  most recent 95 daily rows, so the IPO month is not retrievable from it. The
  chart starts at 2026-05-01 as a result. Backfilling requires a different
  source.
- The Lumina newsroom HTML scraper is not implemented yet, so company news
  currently comes from the Yahoo Finance feed only. Social sources (YouTube, X)
  are also not wired up.
- Metal prices depend on a manual upload; if no new file is provided the
  previous values are shown and the "updated on" date will not advance.

## Notes

`index.html` is fully self-contained — the charting library and all data are
inlined, so the page renders with no network access. Open it directly from
disk and it works offline.
