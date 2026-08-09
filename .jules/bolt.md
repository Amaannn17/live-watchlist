## 2024-05-24 - Avoiding innerHTML Equality Checks on Polled Data
**Learning:** Checking `element.innerHTML !== newHTML` to prevent unnecessary DOM updates is unreliable and expensive because the browser serializes the DOM nodes into a string which might not exactly match the originally assigned raw HTML string. This can cause redundant DOM updates during polling cycles.
**Action:** Cache the generated raw HTML string in a custom property on the DOM element (e.g., `element._rawHtml`) and use that for equality checks before updating `innerHTML`.

## 2024-05-25 - Skip JSON parsing on unchanged polling responses
**Learning:** In polling applications, to avoid redundant `JSON.parse()` calls and subsequent data processing when data hasn't changed, we can cache the raw response string (`await response.text()`) and compare it against the incoming response, returning early if they match. Always clear this cache inside error/catch blocks to ensure proper application recovery upon network restoration.
**Action:** Cache the raw text from polling API responses, compare with the previous response text to avoid parsing and rendering when the response is identical.
