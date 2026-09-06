## 2024-05-24 - Avoiding innerHTML Equality Checks on Polled Data
**Learning:** Checking `element.innerHTML !== newHTML` to prevent unnecessary DOM updates is unreliable and expensive because the browser serializes the DOM nodes into a string which might not exactly match the originally assigned raw HTML string. This can cause redundant DOM updates during polling cycles.
**Action:** Cache the generated raw HTML string in a custom property on the DOM element (e.g., `element._rawHtml`) and use that for equality checks before updating `innerHTML`.

## 2024-05-24 - Avoiding Redundant JSON Processing on Polled Data
**Learning:** In polling applications, `JSON.parse()` and subsequent data processing can be a significant overhead when data hasn't changed. Comparing the incoming raw response string (`await response.text()`) against a cached copy of the previous response allows the application to return early, bypassing parsing and DOM updates entirely.
**Action:** Cache the raw text string from the network response and compare it against the incoming response string, breaking out early if they match. Always clear the cache inside error/catch blocks to guarantee proper data processing upon recovery.

## 2024-09-06 - Row-Level Memoization on Polled Data
**Learning:** In polling applications, even if the raw response string changes (e.g., one row updated), processing and re-rendering all rows is expensive (O(N)). Memoizing individual data items via a lightweight signature allows short-circuiting unchanged rows.
**Action:** Generate a data signature (e.g., via `JSON.stringify` of the raw row) and cache it on the corresponding DOM element. Bypass processing and rendering logic if the signature hasn't changed.
