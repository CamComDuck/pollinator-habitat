# For Future Teams

This document lists known issues and improvement opportunities identified during the final iteration of the Pollinator Habitat project. Items are organized by category for easy prioritization.

---

## Known Issues

### 1. Portal Route Stats — Session ID Mode Shows Incomplete Data

The Route Data Tool in the Admin Portal shows correct results when searching by **date or date range**. When searching by **Session ID**, the Activity Overview table populates correctly, but the Positive Trends and Missed Opportunities tables display zeros.

The backend has 10 session-scoped route statistics endpoints fully implemented (see `ROUTE_STATS_API_REFERENCE.md` in the source code repo), but the portal's `routeDatafetchService.ts` only calls the date-range versions of those endpoints. The session-ID variants need to be wired to the corresponding fetch functions and passed into the `PositiveTrendsTable` and `MissedOpportunitiesTable` components on the Route page.

---

## Improvements for Future Teams

### 1. Portal Quick Export: Add a "Both" Option

The Quick Export Tool (`portal/src/app/export/page.tsx`) only allows selecting "Survey Report" or "Route Report" — one at a time. The client requested a "Both" option that triggers both exports sequentially with a single button press, producing two separate CSV files. The `selectedData` state would need to support a third value (e.g., `"both"`), and `handleExport` would need to run both the survey and route export paths in sequence.

### 2. Accessibility Settings Lost on Hard Refresh

Accessibility settings (high contrast, TTS, font size) are saved to `localStorage` and applied as CSS classes/custom properties by `accessibility/page.tsx` — but only when that page is visited. The root `layout.tsx` is a server component and does not read localStorage. This means on a hard refresh or new tab, settings appear reset until the user navigates back to the accessibility page.

The fix is to add a small client component to `layout.tsx` that reads `localStorage['accessibilitySettings']` on mount and applies the `high-color-contrast` class, `TTS-option-switch` class, and `--font-scale` custom property to `document.documentElement` immediately — replicating what `accessibility/page.tsx` already does.

### 3. Portal Route Data Tool: Wire Session-Based Stats for Trends and Missed Opportunities

When the Route Data Tool searches by Session ID (`portal/src/app/route/page.tsx`, lines 88–99), only two backend calls are made (`fetchTotalRoutesCompletedBySession`, `fetchTotalConnectedUsersBySession`). The `avgRoutesPerUser` and `avgRoutesPerSession` fields are hardcoded to 0, and the Positive Trends and Missed Opportunities tables are left empty.

The backend has session-scoped endpoints for all remaining metrics, but the corresponding fetch functions do not yet exist in `portal/src/services/routeDatafetchService.ts`. Adding those fetch functions and wiring them into the session-ID branch of `handleSearch` would complete the feature.
