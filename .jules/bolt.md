## 2024-05-24 - Avoiding innerHTML Equality Checks on Polled Data
**Learning:** Checking `element.innerHTML !== newHTML` to prevent unnecessary DOM updates is unreliable and expensive because the browser serializes the DOM nodes into a string which might not exactly match the originally assigned raw HTML string. This can cause redundant DOM updates during polling cycles.
**Action:** Cache the generated raw HTML string in a custom property on the DOM element (e.g., `element._rawHtml`) and use that for equality checks before updating `innerHTML`.

## 2024-05-24 - Avoiding Redundant Data Parsing on Polled Data
**Learning:** Polling mechanisms that frequently fetch data from an endpoint often perform unnecessary JSON parsing and processing when the data hasn't actually changed, which blocks the main thread and degrades frontend performance.
**Action:** In polling applications, to avoid redundant `JSON.parse()` calls and subsequent data processing when data hasn't changed, cache the raw response string (`await response.text()`) and compare it against the incoming response, returning early if they match.
