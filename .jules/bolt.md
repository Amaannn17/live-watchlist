## 2024-05-24 - Avoiding innerHTML Equality Checks on Polled Data
**Learning:** Checking `element.innerHTML !== newHTML` to prevent unnecessary DOM updates is unreliable and expensive because the browser serializes the DOM nodes into a string which might not exactly match the originally assigned raw HTML string. This can cause redundant DOM updates during polling cycles.
**Action:** Cache the generated raw HTML string in a custom property on the DOM element (e.g., `element._rawHtml`) and use that for equality checks before updating `innerHTML`.

## 2024-05-24 - Avoiding Redundant JSON Processing on Polled Data
**Learning:** In polling applications, `JSON.parse()` and subsequent data processing can be a significant overhead when data hasn't changed. Comparing the incoming raw response string (`await response.text()`) against a cached copy of the previous response allows the application to return early, bypassing parsing and DOM updates entirely.
**Action:** Cache the raw text string from the network response and compare it against the incoming response string, breaking out early if they match. Always clear the cache inside error/catch blocks to guarantee proper data processing upon recovery.

## 2024-05-24 - Avoiding Expensive String Interpolation in Polling Lists
**Learning:** Checking `element.innerHTML !== newHTML` alone isn't enough when rendering lists of complex items (like stock cards with manual logs). The process of building `newHTML` (regex replacements, looping over arrays, string concatenations) for *every* item in the list on *every* poll is wasteful, especially when only one item's data actually changed.
**Action:** Implement data-level memoization. Generate a lightweight data signature (e.g., `JSON.stringify` of raw data inputs) before generating the HTML string. Compare this signature with a cached version on the DOM element (`element._rowSignature`) and return early if they match, skipping the expensive HTML generation step entirely.
