## 2024-05-24 - Unreliable `innerHTML` comparisons
**Learning:** Comparing `element.innerHTML` to a raw HTML string is unreliable for determining if an update is needed. This is because the browser parses the string and serializes it back to HTML, which might differ from the original string (e.g. attribute ordering, quote normalization).
**Action:** Instead of checking `element.innerHTML === newInnerHTML`, cache the raw HTML string on a custom property (e.g. `element._rawHtml = newInnerHTML`) and use that for equality checks to prevent redundant DOM updates during polling cycles.
