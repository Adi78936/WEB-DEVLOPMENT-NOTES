# HTML Advanced Concepts — Interview Preparation

## 1. Meta tags

`<meta>` elements provide document metadata that is not usually displayed as page content. They are placed in the document's `<head>`.

```html
<head>
  <meta charset="UTF-8">
  <meta name="description" content="Notes on retinal image processing.">
  <meta name="author" content="Research team">
</head>
```

Common metadata includes:

- Character encoding, usually `<meta charset="UTF-8">`.
- A description for the page.
- Viewport behavior for mobile layouts.
- Platform-specific or application metadata when relevant.

The charset declaration should appear near the beginning of the document. Meta tags provide information; they do not themselves guarantee that a browser, search engine, or social platform will behave in a particular way.

## 2. Viewport meta tag

The viewport meta tag helps a mobile browser use the device's actual viewport width:

```html
<meta name="viewport" content="width=device-width, initial-scale=1">
```

- `width=device-width` sets the layout viewport width to the device's width.
- `initial-scale=1` sets the initial zoom scale.
- Without an appropriate viewport declaration, mobile browsers may use a wider virtual layout viewport and scale the page down.
- Avoid disabling zoom with `user-scalable=no` or restrictive `maximum-scale` values. Users may need to zoom to read content.

The viewport declaration does not make a page responsive by itself; responsive layout still requires suitable CSS.

## 3. SEO-related metadata

Search engines use many signals to understand and rank pages; metadata alone does not guarantee indexing or a particular ranking.

### Title and description

```html
<title>Retinal Image Processing — Project Notes</title>
<meta
  name="description"
  content="A research project exploring retinal image preprocessing and diabetic retinopathy classification.">
```

- `<title>` names the document and commonly appears in browser tabs and search results.
- A description can be used as a search-result summary, but search engines may choose other page text.
- Make titles and descriptions accurate and specific to the page. Avoid repetitive keyword stuffing.

### Canonical URL

When a page has multiple URLs that represent the same content, a canonical link can indicate the preferred URL:

```html
<link rel="canonical" href="https://example.org/project-notes">
```

Set a canonical URL only when it is correct for the page. A wrong canonical can direct search engines to an unintended URL.

### Open Graph and sharing metadata

Open Graph metadata can provide title, description, and image information to services that use it for link previews:

```html
<meta property="og:type" content="website">
<meta property="og:title" content="Retinal Image Processing">
<meta property="og:description" content="Project overview and research workflow.">
<meta property="og:url" content="https://example.org/project">
<meta property="og:image" content="https://example.org/images/project-preview.jpg">
```

Social platforms may cache previews or apply their own rules. A metadata tag cannot guarantee how every service displays a shared link.

### Robots metadata

The `robots` meta tag can communicate crawler directives:

```html
<meta name="robots" content="noindex, nofollow">
```

Use directives only when intended, and understand their scope. They are instructions to compliant crawlers, not access control. Do not rely on `noindex` or `robots.txt` to protect private pages; use authentication and authorization for restricted content.

## 4. Favicon

A favicon is a small site icon that browsers may display in tabs, bookmarks, and other browser interfaces. Link to it from the document head:

```html
<link rel="icon" href="/favicon.ico" sizes="any">
<link rel="icon" href="/icon.svg" type="image/svg+xml">
<link rel="apple-touch-icon" href="/apple-touch-icon.png">
```

- The file must exist at the referenced URL and be in a format the target browsers support.
- Providing multiple formats or sizes can support different contexts.
- A favicon improves site identification but is not a substitute for the document title.

## 5. HTML5 APIs overview

HTML is the markup language; many features commonly called “HTML5 APIs” are browser APIs available to JavaScript. They are not all HTML tags, and support or requirements vary by browser.

Examples include:

- **Canvas:** the `<canvas>` element and Canvas API draw or manipulate graphics using JavaScript.
- **Geolocation:** the Geolocation API can request a user's location, subject to permission and secure-context requirements.
- **Drag and drop:** HTML drag-and-drop events support drag interactions; accessible alternatives may also be needed.
- **Media:** `<audio>` and `<video>` provide media elements, and JavaScript APIs can control playback.
- **Web Storage:** `localStorage` and `sessionStorage` store strings in the browser.
- **History:** the History API can update session history for client-side navigation.
- **Web Workers:** run certain JavaScript tasks in a separate worker thread to avoid blocking the main interface.

When using browser APIs:

- Check compatibility and relevant security or permission requirements.
- Handle denied permissions, unavailable features, and errors.
- Keep accessible, usable alternatives for essential actions.
- Do not assume an API is available just because the browser supports HTML.

## 6. Data attributes

Custom `data-*` attributes let authors attach application-specific data to an HTML element:

```html
<button type="button" data-action="remove-image" data-image-id="sample-12">
  Remove image
</button>
```

JavaScript can access these values through an element's `dataset`:

```js
const button = document.querySelector("[data-action]");
console.log(button.dataset.action);  // "remove-image"
console.log(button.dataset.imageId); // "sample-12"
```

Important details:

- Attribute names use lowercase HTML syntax after `data-`; hyphenated names become camelCase in `dataset`.
- Dataset values are strings. Parse and validate a value before using it as a number, boolean, or other type.
- Use `data-*` for small, element-specific application data—not as a replacement for semantic HTML, accessible names, or a full data store.
- Do not place secrets or sensitive information in data attributes; they are part of the page and can be inspected.

## 7. Script loading: `defer` and `async`

External classic scripts without either attribute can pause HTML parsing while the browser fetches and executes the script. `defer` and `async` change this behavior.

### `defer`

```html
<script src="/js/app.js" defer></script>
```

- The browser downloads the external script while parsing HTML.
- The script executes after HTML parsing has finished and before `DOMContentLoaded`.
- Deferred classic scripts execute in document order.
- Use `defer` when a script depends on the parsed document or on earlier deferred scripts.
- `defer` has no effect on inline classic scripts. Module scripts are deferred by default unless marked `async`.

### `async`

```html
<script src="/js/analytics.js" async></script>
```

- The browser downloads the script while parsing HTML.
- It executes as soon as it is ready, potentially interrupting parsing.
- The order of multiple async scripts is not guaranteed.
- Use it for independent scripts that do not depend on other scripts' execution order or on a fully parsed document.

### Quick comparison

| Behavior | `defer` | `async` |
|---|---|---|
| Download while HTML parses | Yes | Yes |
| Execute after parsing is complete | Yes | Not necessarily |
| Preserve order between same-type classic scripts | Yes, document order | No guaranteed order |
| Typical use | App scripts that need the parsed DOM and ordered dependencies | Independent scripts with no ordering dependency |

Always use the appropriate `src` and test the behavior of dependent scripts. Loading attributes do not remove the need to handle failures or unavailable resources.

## 8. `localStorage` overview

`localStorage` is a browser Web Storage area associated with an origin. Its data generally persists across page reloads and browser restarts until it is cleared or removed.

```js
localStorage.setItem("theme", "dark");

const theme = localStorage.getItem("theme");

localStorage.removeItem("theme");
// localStorage.clear(); // Removes every key for this origin.
```

Key points:

- Keys and values are stored as strings.
- Use `JSON.stringify()` and `JSON.parse()` when storing structured data, and handle invalid or outdated stored values.
- It is synchronous, so large or frequent operations can block the main thread.
- Available storage and quotas vary. Operations can fail, so catch and handle storage errors where appropriate.
- Data is scoped by origin, not shared freely across different origins.
- Same-origin JavaScript can read it. Do not store passwords, session secrets, or other sensitive data in it.
- It may be unavailable or restricted in some browsing contexts.

## 9. `sessionStorage` overview

`sessionStorage` is a browser Web Storage area associated with an origin and a top-level browsing context (usually a tab). It normally lasts for the lifetime of that page session; reloading the page keeps the data, while closing the tab ends the session.

```js
sessionStorage.setItem("active-view", "pipeline");

const activeView = sessionStorage.getItem("active-view");

sessionStorage.removeItem("active-view");
```

Key points:

- It has a similar string-based API to `localStorage`.
- Data is separated by origin and browsing context.
- It is useful for short-lived tab-specific state, not as secure storage.
- Browser behavior can copy an initial session in some cases, such as a new window opened with an opener; do not treat session storage as an isolation or security boundary.
- Storage access can fail or be restricted, so handle errors and provide a sensible fallback.

## 10. Choosing between Web Storage and alternatives

- Use `localStorage` for small, non-sensitive preferences that should survive a browser restart.
- Use `sessionStorage` for small, non-sensitive, tab-scoped state that can be discarded after the session.
- Web Storage stores strings synchronously; it is not appropriate for large datasets or high-frequency writes.
- IndexedDB is a better browser-side option for larger structured data and asynchronous operations.
- Server-side storage is needed when data should be associated with an account, shared across devices, or reliably backed up.
- Browser storage is not a security boundary: same-origin JavaScript, including injected scripts, may be able to access it.

## Quick interview review

1. **What does the viewport meta tag do?**  
   It tells mobile browsers to use the device viewport width and initial scale; responsive CSS is still needed.

2. **Does a meta description guarantee the same search-result snippet?**  
   No. Search engines may choose other page text and use many signals.

3. **What is a canonical link for?**  
   It indicates a preferred URL for equivalent or duplicate page content; it must point to the correct page.

4. **Do `async` and `defer` work the same way?**  
   No. Deferred classic scripts run after parsing in document order; async scripts run as soon as available, with no guaranteed order.

5. **How do `localStorage` and `sessionStorage` differ?**  
   `localStorage` generally persists until cleared; `sessionStorage` is scoped to a tab's page session.

6. **Are values in Web Storage typed?**  
   No. The API stores string key-value pairs; the application must serialize and parse structured values.

7. **Is Web Storage safe for secrets?**  
   No. Same-origin JavaScript can read it, so do not store passwords or sensitive authentication tokens there.

8. **What are `data-*` attributes for?**  
   Small custom data associated with an HTML element; JavaScript reads them as strings through `dataset`.

9. **Is the Geolocation API simply an HTML element?**  
   No. It is a browser API accessed through JavaScript and subject to permission and security requirements.

## Good practices to remember

- Use meaningful, accurate titles, descriptions, and sharing metadata.
- Set a mobile-friendly viewport but preserve user zoom.
- Treat crawler metadata as guidance, not access control or a ranking guarantee.
- Use `defer` for ordered scripts that need the parsed document; use `async` only for independent scripts.
- Keep `data-*` values small, non-sensitive, and validated before use.
- Use Web Storage for small, non-sensitive values and handle unavailable storage.
- Do not treat browser storage as private, durable, or shared server storage.
- Check API support, permissions, errors, and accessible alternatives.
