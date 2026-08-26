## 2024-05-24 - Avoiding innerHTML Equality Checks on Polled Data
**Learning:** Checking `element.innerHTML !== newHTML` to prevent unnecessary DOM updates is unreliable and expensive because the browser serializes the DOM nodes into a string which might not exactly match the originally assigned raw HTML string. This can cause redundant DOM updates during polling cycles.
**Action:** Cache the generated raw HTML string in a custom property on the DOM element (e.g., `element._rawHtml`) and use that for equality checks before updating `innerHTML`.

## 2024-05-24 - Avoiding Redundant JSON Processing on Polled Data
**Learning:** In polling applications, `JSON.parse()` and subsequent data processing can be a significant overhead when data hasn't changed. Comparing the incoming raw response string (`await response.text()`) against a cached copy of the previous response allows the application to return early, bypassing parsing and DOM updates entirely.
**Action:** Cache the raw text string from the network response and compare it against the incoming response string, breaking out early if they match. Always clear the cache inside error/catch blocks to guarantee proper data processing upon recovery.

## 2024-05-24 - Avoiding Expensive String Operations on Unchanged Polled Data
**Learning:** During polling cycles, extracting values and generating HTML for unchanged individual data rows is a waste of CPU cycles, particularly when the overall network payload might have changed due to other rows updating.
**Action:** Generate a lightweight data signature for each row (e.g., `JSON.stringify(row)`) and cache it on the DOM element (`card._rowSignature`). By comparing this signature before data processing, we can short-circuit the execution and bypass expensive regex operations and HTML string generation entirely for unchanged data rows.
