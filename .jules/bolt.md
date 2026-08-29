## 2024-05-24 - Avoiding innerHTML Equality Checks on Polled Data
**Learning:** Checking `element.innerHTML !== newHTML` to prevent unnecessary DOM updates is unreliable and expensive because the browser serializes the DOM nodes into a string which might not exactly match the originally assigned raw HTML string. This can cause redundant DOM updates during polling cycles.
**Action:** Cache the generated raw HTML string in a custom property on the DOM element (e.g., `element._rawHtml`) and use that for equality checks before updating `innerHTML`.

## 2024-05-24 - Avoiding Redundant JSON Processing on Polled Data
**Learning:** In polling applications, `JSON.parse()` and subsequent data processing can be a significant overhead when data hasn't changed. Comparing the incoming raw response string (`await response.text()`) against a cached copy of the previous response allows the application to return early, bypassing parsing and DOM updates entirely.
**Action:** Cache the raw text string from the network response and compare it against the incoming response string, breaking out early if they match. Always clear the cache inside error/catch blocks to guarantee proper data processing upon recovery.

## 2024-05-24 - Data-level Memoization for Polled Data Rows
**Learning:** In polling applications, even if the overall payload changes, individual data rows often remain identical. Processing unchanged data wastes CPU cycles on regex and string building.
**Action:** Implement data-level memoization by generating a lightweight data signature (e.g., via `JSON.stringify` of raw inputs) and caching it on the DOM element (e.g., `card._rowSignature`). This allows the application to short-circuit and bypass expensive HTML string generation and regex operations entirely for unchanged data.
