# csvExportService.ts — Line-by-Line Reference

## File Purpose

Browser-side CSV generation and download. Takes in-memory data rows and triggers a file download without any server round-trip. Exports two functions — one for survey data and one for route stats — that both follow the same download pattern.

---

## Line-by-Line Breakdown

### Lines 1–2 — Imports

```ts
import type { SurveyDataRow } from "./surveyDatafetchService";
import type { RouteStatRow } from "./routeDataFetchService";
```

Type-only imports so the module has no runtime dependency on either service. Only the shape of the row objects is needed here.

---

### Lines 4–23 — `exportToCsv`

```ts
export function exportToCsv(filename: string, rows: SurveyDataRow[])
```

Builds and downloads a CSV of survey results (session ID, date, adults, children, total).

| Lines | What happens |
|---|---|
| 5 | Defines the column headers: `Session ID`, `Date`, `Adults`, `Children`, `Total` |
| 6–11 | Maps each `SurveyDataRow` to a comma-joined string. `numAdults`/`numChildren` are coerced to numbers (defaulting to `0` if blank/null), and `total` is computed as their sum |
| 13 | Joins the header row and all data rows with newlines into a single CSV string |
| 14 | Wraps the string in a `Blob` with `text/csv;charset=utf-8;` MIME type |
| 15 | Creates a temporary object URL pointing to the blob |
| 16–20 | Creates a hidden `<a>` element, sets its `href` and `download` attribute, appends it to the DOM, clicks it to trigger the browser download, then removes it |
| 22 | Revokes the object URL to free memory |

---

### Lines 25–38 — `exportRouteStatsToCsv`

```ts
export function exportRouteStatsToCsv(filename: string, rows: RouteStatRow[])
```

Same download mechanism as `exportToCsv`, but for route stat rows (metric name + value).

| Lines | What happens |
|---|---|
| 26 | Headers: `Metric`, `Value` |
| 27 | Each row is `"metric label"`,`value` — the metric is wrapped in quotes to handle commas in label text |
| 28–37 | Identical blob → object URL → hidden link → click → cleanup pattern as above |

---

## Summary

| Export | Input rows | CSV columns | Called from |
|---|---|---|---|
| `exportToCsv` | `SurveyDataRow[]` | Session ID, Date, Adults, Children, Total | `survey/page.tsx` Export button, `export/page.tsx` Survey Report |
| `exportRouteStatsToCsv` | `RouteStatRow[]` | Metric, Value | `export/page.tsx` Route Report |

Both functions are synchronous and browser-only — they rely on `document` and `URL.createObjectURL`, so they cannot be called in a server context.
