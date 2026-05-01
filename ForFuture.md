# For Future Teams

This document lists known issues and improvement opportunities identified during the final iteration of the Pollinator Habitat project. Items are organized by category for easy prioritization.

---

## Known Issues

None

---

## Improvements for Future Teams

### 1. Portal Quick Export: Add a "Both" Option

The Quick Export Tool (`portal/src/app/export/page.tsx`) only allows selecting "Survey Report" or "Route Report" — one at a time. The client requested a "Both" option that triggers both exports sequentially with a single button press, producing two separate CSV files. The `selectedData` state would need to support a third value (e.g., `"both"`), and `handleExport` would need to run both the survey and route export paths in sequence.

### 2. Accessibility Settings Lost on Hard Refresh

Accessibility settings (high contrast, TTS, font size) are saved to `localStorage` and applied as CSS classes/custom properties by `accessibility/page.tsx` — but only when that page is visited. The root `layout.tsx` is a server component and does not read localStorage. This means on a hard refresh or new tab, settings appear reset until the user navigates back to the accessibility page.

The fix is to add a small client component to `layout.tsx` that reads `localStorage['accessibilitySettings']` on mount and applies the `high-color-contrast` class, `TTS-option-switch` class, and `--font-scale` custom property to `document.documentElement` immediately — replicating what `accessibility/page.tsx` already does.

