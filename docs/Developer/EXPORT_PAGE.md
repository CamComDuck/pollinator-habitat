# export/page.tsx — Line-by-Line Reference

## File Purpose

The Quick Export Tool page. Staff select a **reporting period** (1 month → all time) and a **data type** (Survey or Route), then click a single button to fetch and download a CSV. No table is shown — the export fires directly to the browser's download prompt.

---

## Line-by-Line Breakdown

### Lines 1–8 — Directives and Imports

```ts
"use client";
```

Client component — required for `useState` and event handlers.

Imports:
- UI components from `components.tsx`: logo, header, buttons, checkboxes, labels
- `fetchSurveyDataByDateRange` from `surveyDatafetchService.ts` — used for Survey Report exports
- `fetchRouteStatsByDateRange` from `routeDataFetchService.ts` — used for Route Report exports
- `exportToCsv`, `exportRouteStatsToCsv` from `csvExportService.ts` — trigger the download

---

### Lines 10–21 — `periodToStartDate` (helper)

```ts
function periodToStartDate(period: string): string
```

Converts a period key into a start date string (`YYYY-MM-DD`). The end date is always today.

| Period key | Start date |
|---|---|
| `"1month"` | 1 month ago |
| `"3months"` | 3 months ago |
| `"6months"` | 6 months ago |
| `"1year"` | 1 year ago |
| `"3years"` | 3 years ago |
| `"alltime"` | `"2020-01-01"` (hardcoded project epoch) |

Uses `setMonth`/`setFullYear` on a `new Date()` instance, then returns `toISOString().slice(0, 10)`.

---

### Lines 23–28 — State Declarations

| State | Initial | Purpose |
|---|---|---|
| `selectedPeriod` | `null` | Which period checkbox is active (`"1month"`, `"3months"`, etc.) |
| `selectedData` | `null` | Which data type is selected (`"survey"` or `"route"`) |
| `loading` | `false` | Disables the Export button during the fetch |
| `error` | `null` | Error message shown below the Export button |

---

### Line 30 — `canExport`

```ts
const canExport = selectedPeriod !== null && selectedData !== null;
```

Both a period and a data type must be selected before the Export button is enabled.

---

### Lines 32–51 — `handleExport`

```ts
async function handleExport()
```

The export handler:

| Lines | What happens |
|---|---|
| 33 | Guards: returns early if either selection is missing |
| 36 | Converts `selectedPeriod` to a start date via `periodToStartDate` |
| 37 | Sets end date to today |
| 39–41 | If `selectedData === "survey"`: fetches survey rows and calls `exportToCsv` |
| 42–45 | Otherwise (route): fetches route stat rows and calls `exportRouteStatsToCsv` |
| 46–48 | Catches any error and stores it in `error` state |
| 49–50 | `finally` clears `loading` |

The CSV filename includes the period key (e.g., `survey-report-3months.csv`, `route-report-1year.csv`).

---

### Lines 53–106 — JSX Layout

The page is structured as a `<table className="page_table">` with these rows:

| Row | Contents |
|---|---|
| Logo row | `LogoImage` |
| Nav row | `HomeButton` → `/menu` |
| Header row | `PortalHeader` — "Quick Export Tool" |
| Options row | Two columns (period + data type) each with `SearchHeader`, `ExportText`, and `OptionCheckbox` groups |
| Export row | `InteractiveButton` + optional error `<span>` |

**Period column (left, lines 73–79):** Six `OptionCheckbox` components, one per period. Each uses `checked={selectedPeriod === "<key>"}` and `onChange={(val) => setSelectedPeriod(val ? "<key>" : null)}` — checking one automatically unchecks the others because only one string can equal `selectedPeriod` at a time.

**Data type column (right, lines 86–93):** Two `OptionCheckbox` components for Survey and Route, using the same single-select pattern with `selectedData`.

**Export button (line 99):**
- Label switches to `"Exporting..."` while `loading` is true
- `disabled={!canExport || loading}` — blocked until both selections are made and no fetch is in flight
- Error message rendered inline with `role="alert"` if present (line 100)

---

## Summary

| Concern | Handled by |
|---|---|
| Period → date conversion | `periodToStartDate` |
| Single-select checkbox groups | `selectedPeriod`/`selectedData` string state compared per checkbox |
| Survey data fetch | `fetchSurveyDataByDateRange` |
| Route stats fetch | `fetchRouteStatsByDateRange` |
| CSV download | `exportToCsv` / `exportRouteStatsToCsv` |
| Navigation | `useRouter` → `/menu` via `HomeButton` |
