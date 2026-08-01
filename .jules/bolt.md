## 2024-05-24 - Avoiding innerHTML Equality Checks on Polled Data
**Learning:** Checking `element.innerHTML !== newHTML` to prevent unnecessary DOM updates is unreliable and expensive because the browser serializes the DOM nodes into a string which might not exactly match the originally assigned raw HTML string. This can cause redundant DOM updates during polling cycles.
**Action:** Cache the generated raw HTML string in a custom property on the DOM element (e.g., `element._rawHtml`) and use that for equality checks before updating `innerHTML`.

## 2024-05-24 - Avoiding Redundant Parsing in Polling Cycles
**Learning:** In polling applications, `JSON.parse()` and subsequent data processing can be expensive and unnecessary if the remote data hasn't changed.
**Action:** Cache the raw response string (`await response.text()`) and compare it against the incoming response string to early-exit the polling cycle if the data is identical. Always clear this cache inside error/catch blocks to ensure application recovery upon network restoration.
