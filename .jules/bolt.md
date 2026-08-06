## 2024-05-24 - Avoiding innerHTML Equality Checks on Polled Data
**Learning:** Checking `element.innerHTML !== newHTML` to prevent unnecessary DOM updates is unreliable and expensive because the browser serializes the DOM nodes into a string which might not exactly match the originally assigned raw HTML string. This can cause redundant DOM updates during polling cycles.
**Action:** Cache the generated raw HTML string in a custom property on the DOM element (e.g., `element._rawHtml`) and use that for equality checks before updating `innerHTML`.

## 2024-05-14 - Optimize polling logic and raw HTML caching
**Learning:** Polling applications inherently waste CPU cycles re-parsing and re-rendering identical data. `innerHTML` comparisons are slow and unreliable due to browser normalization.
**Action:** Implemented a raw string caching strategy. First, cache `await response.text()` and abort early if it matches the previous poll. Second, cache the generated string in `element._rawHtml` rather than relying on `innerHTML` equality checks for DOM updates. This prevents unnecessary JSON parsing and DOM thrashing.
