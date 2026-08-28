## 2024-05-24 - Avoiding innerHTML Equality Checks on Polled Data
**Learning:** Checking `element.innerHTML !== newHTML` to prevent unnecessary DOM updates is unreliable and expensive because the browser serializes the DOM nodes into a string which might not exactly match the originally assigned raw HTML string. This can cause redundant DOM updates during polling cycles.
**Action:** Cache the generated raw HTML string in a custom property on the DOM element (e.g., `element._rawHtml`) and use that for equality checks before updating `innerHTML`.

## 2024-05-24 - Avoiding Redundant JSON Processing on Polled Data
**Learning:** In polling applications, `JSON.parse()` and subsequent data processing can be a significant overhead when data hasn't changed. Comparing the incoming raw response string (`await response.text()`) against a cached copy of the previous response allows the application to return early, bypassing parsing and DOM updates entirely.
**Action:** Cache the raw text string from the network response and compare it against the incoming response string, breaking out early if they match. Always clear the cache inside error/catch blocks to guarantee proper data processing upon recovery.

## 2024-05-24 - Avoiding Redundant Object Parsing on Polled Data
**Learning:** Generating HTML strings and performing regex parsing for every object in a polled array is expensive, even if the result isn't written to the DOM.
**Action:** Implement data-level memoization by computing a lightweight signature (like `JSON.stringify(row)`) and caching it on the DOM element (`card._rowSignature`). This allows skipping the entire HTML generation phase for data that hasn't changed.
