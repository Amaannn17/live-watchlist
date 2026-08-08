## 2024-05-24 - Avoiding innerHTML Equality Checks on Polled Data
**Learning:** Checking `element.innerHTML !== newHTML` to prevent unnecessary DOM updates is unreliable and expensive because the browser serializes the DOM nodes into a string which might not exactly match the originally assigned raw HTML string. This can cause redundant DOM updates during polling cycles.
**Action:** Cache the generated raw HTML string in a custom property on the DOM element (e.g., `element._rawHtml`) and use that for equality checks before updating `innerHTML`.
## 2024-05-24 - Avoiding Redundant JSON Processing in Polling Apps
**Learning:** Parsing JSON (`await response.json()`) and processing the data on every poll cycle is inefficient when data hasn't changed.
**Action:** Cache the raw response string (`await response.text()`) and compare it against the incoming response string, returning early if they match. Clear the cache inside the error/catch blocks to allow proper recovery.
