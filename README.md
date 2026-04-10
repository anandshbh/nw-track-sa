# 📈 Investment Value Track

> A personal mutual fund portfolio tracker — automated, always up to date, and beautifully visualised.

**Live site →** [https://www.cloudquip.com/](https://www.cloudquip.com/)

---

## What it does

This is a lightweight, single-file dashboard that tracks the daily grand total value of a mutual fund portfolio — sourced automatically from Gmail and visualised as an interactive chart with a full data table.

Every day, a Google Sheet sends an automated email with the current portfolio value. This tracker reads those emails and plots the journey.

---

## Features

- **Daily value tracking** — one data point per day, pulled from Gmail
- **Interactive line chart** — powered by Chart.js, with hover tooltips showing value and daily change
- **Full data table** — every date listed with its value and the change from the previous day
- **MAX / MIN highlights** — the highest and lowest values in the dataset are colour-highlighted in both the chart and the table
- **INR formatting** — all values displayed in Indian Rupee format with proper locale formatting
- **Zero dependencies to run** — a single `index.html` file; works offline in any browser

---

## How it's built

| Layer | Technology |
|---|---|
| Dashboard | Plain HTML + CSS + JavaScript |
| Chart | [Chart.js 4.4.1](https://www.chartjs.org/) via CDN |
| Data source | Gmail — daily email with subject `Daily Sheet Update - Grand Total` |
| Hosting | GitHub Pages |
| Updates | Manual (via Claude AI + Gmail MCP) |

---

## Data source

Each day, a Google Apps Script attached to a personal Google Sheet sends an email in this format:

```
Hello, Your Grand Total (Cell D21) is: 2355510 This email was sent from your Google Sheet.
```

The numeric value between `is:` and `This` is extracted and added as a new row in the tracker.

---

## Project structure

```
nw-track-sa/
├── index.html          # The entire dashboard — chart, table, styles, and data
├── CNAME               # Custom domain config for GitHub Pages
└── assets/
    ├── favicon.ico
    ├── favicon.svg
    ├── favicon-96x96.png
    ├── apple-touch-icon.png
    └── site.webmanifest
```

---

## Updating the tracker

The dashboard data lives inside `index.html` as a plain JavaScript array:

```js
const raw = [
  ["19 Jan 2026", 2621372],
  ["20 Jan 2026", 2623793],
  // ...
];
```

To add new entries, append new `["DD Mon YYYY", value]` rows to this array. The chart, table, MAX/MIN highlights, and metric cards all update automatically.

Updates are managed via Claude AI using the `UPDATE` command — Claude pulls the latest emails via Gmail MCP, calculates the daily changes, and pushes the updated `index.html` to this repo.

---

## Notes on the data

- **Duplicate emails** — When two emails exist for the same date, the later timestamp is used as the canonical value.
- **Coverage** — Data runs from **19 Jan 2026** onwards and grows daily.

---

## Local preview

No build step needed. Just open `index.html` in any browser:

```bash
open index.html
# or
python3 -m http.server 8000  # then visit localhost:8000
```

---

## Author

**Shubhrant Anand** · [@anandshbh](https://x.com/anandshbh) · [github.com/anandshbh](https://github.com/anandshbh)

---
