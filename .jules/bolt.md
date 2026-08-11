## 2024-05-24 - Avoiding innerHTML Equality Checks on Polled Data
**Learning:** Checking `element.innerHTML !== newHTML` to prevent unnecessary DOM updates is unreliable and expensive because the browser serializes the DOM nodes into a string which might not exactly match the originally assigned raw HTML string. This can cause redundant DOM updates during polling cycles.
**Action:** Cache the generated raw HTML string in a custom property on the DOM element (e.g., `element._rawHtml`) and use that for equality checks before updating `innerHTML`.

## 2024-05-24 - Caching Raw Responses to Avoid Redundant Processing
**Learning:** In polling applications, repeatedly calling `response.json()` and processing the data when the underlying API response hasn't changed causes unnecessary CPU overhead and potential redundant DOM manipulation logic execution.
**Action:** Cache the raw response string (`await response.text()`) and compare it against the incoming response. If they match, return early. Always clear this cache inside error/catch blocks to ensure the application recovers correctly when the network is restored.