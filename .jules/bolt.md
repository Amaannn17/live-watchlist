## 2024-05-24 - Avoiding innerHTML Equality Checks on Polled Data
**Learning:** Checking `element.innerHTML !== newHTML` to prevent unnecessary DOM updates is unreliable and expensive because the browser serializes the DOM nodes into a string which might not exactly match the originally assigned raw HTML string. This can cause redundant DOM updates during polling cycles.
**Action:** Cache the generated raw HTML string in a custom property on the DOM element (e.g., `element._rawHtml`) and use that for equality checks before updating `innerHTML`.

## 2024-05-24 - Avoiding Redundant JSON Processing on Polled Data
**Learning:** In polling applications, `JSON.parse()` and subsequent data processing can be a significant overhead when data hasn't changed. Comparing the incoming raw response string (`await response.text()`) against a cached copy of the previous response allows the application to return early, bypassing parsing and DOM updates entirely.
**Action:** Cache the raw text string from the network response and compare it against the incoming response string, breaking out early if they match. Always clear the cache inside error/catch blocks to guarantee proper data processing upon recovery.

## 2024-05-24 - Data-Level Memoization in Polling UI
**Learning:** Even with `innerHTML` string caching, generating massive HTML strings and performing regex replacements on every polling cycle for every row item is an unnecessary CPU bottleneck when only one or two rows might have changed.
**Action:** Implement data-level memoization by caching a lightweight data signature (e.g., `JSON.stringify(row)`) on the DOM element (`element._rowSignature`). Check this signature before generating any HTML to short-circuit the entire rendering function for unchanged rows.
