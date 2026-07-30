## 2024-05-24 - Avoiding innerHTML Equality Checks on Polled Data
**Learning:** Checking `element.innerHTML !== newHTML` to prevent unnecessary DOM updates is unreliable and expensive because the browser serializes the DOM nodes into a string which might not exactly match the originally assigned raw HTML string. This can cause redundant DOM updates during polling cycles.
**Action:** Cache the generated raw HTML string in a custom property on the DOM element (e.g., `element._rawHtml`) and use that for equality checks before updating `innerHTML`.

## 2024-05-24 - Avoiding Redundant JSON Parsing in Polling
**Learning:** In polling applications, `response.json()` and subsequent data processing (like iterating and generating HTML) can be unnecessarily expensive when the data hasn't changed. Comparing the raw response text before parsing is a much cheaper way to check for changes.
**Action:** Cache the raw response string and compare it with `await response.text()`. If unchanged, return early. Only `JSON.parse` if the raw string differs. Remember to reset the cache on network errors to ensure UI recovery.
