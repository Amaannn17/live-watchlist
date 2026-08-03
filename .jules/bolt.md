## 2024-05-24 - Avoiding innerHTML Equality Checks on Polled Data
**Learning:** Checking `element.innerHTML !== newHTML` to prevent unnecessary DOM updates is unreliable and expensive because the browser serializes the DOM nodes into a string which might not exactly match the originally assigned raw HTML string. This can cause redundant DOM updates during polling cycles.
**Action:** Cache the generated raw HTML string in a custom property on the DOM element (e.g., `element._rawHtml`) and use that for equality checks before updating `innerHTML`.

## 2024-05-24 - API Response Caching in Polling Applications
**Learning:** In polling applications, redundant `JSON.parse()` calls and subsequent data processing occur when the fetched data hasn't changed. Parsing JSON and manipulating the DOM on unchanged data is a waste of CPU cycles and battery.
**Action:** Cache the raw response string (`await response.text()`) and compare it against the incoming response string. Return early if they match. Always clear this cache inside error blocks to ensure the application recovers properly when the network connection is restored.
