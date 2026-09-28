# Designing a dashboard or report — numbers people act on

> If the person has design standards of their own — a design system, components, a brand guide, an app or site to match — follow those, and use this playbook only for what they leave open. If they gave none, follow it all.

A sales summary, a spending report, an operations view: people glance at it to answer a few
questions. Start by writing those questions down; every tile and chart answers one of them.

## Shape

- **Top row: the three to five numbers that matter**, each a tile with the value, a label, and
  the change against the previous period — an arrow and a word, not colour alone. Decide what
  "good" is per number: a cost going up is bad.
- **Then the trend** over time, then the breakdowns (by category, by person, by place), then
  the detail table for anyone who wants the rows.
- **Filters** (date range, segment) at the top, reflected in the URL so a link shows the same
  view; every tile shows its own loading skeleton while it updates.

## Numbers

- Compute on the server — `countBy`, `sumBy`, `groupBy` with `bucket` for months — never by
  loading the records into the browser.
- Format with `Intl.NumberFormat` (currency, percent, compact "12.4K") in the reader's locale;
  `tabular-nums`; numeric columns right-aligned with their units.
- Say where a number comes from and how fresh it is ("Updated 2 min ago").

## Charts

- Choose by the question: change over time → line or area; comparing things → bars
  (horizontal when labels are long); parts of a whole → a stacked bar (a pie only for two or
  three parts); spread → a histogram.
- Use the chart colours from the theme (`--chart-1` … `--chart-5`), at most five series; label
  lines directly instead of relying on a legend; bars start at zero; gridlines faint; a tooltip
  with the exact value. shadcn's chart component (`npx shadcn@latest add chart`) reads the
  theme's chart colours.
- Highlight the point: the series that matters in the accent, the rest muted.

## Checks

- Each question on the list is answered on screen without scrolling on a laptop.
- An empty period, one data point, and a huge value all still look right.
- Nothing is told by colour alone; charts have text a screen reader can use.
- A report someone will forward prints cleanly or exports (CSV from the app's data).
- Then the general checklist in the design guide.
