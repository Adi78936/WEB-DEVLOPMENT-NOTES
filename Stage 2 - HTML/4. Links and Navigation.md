# HTML Links and Navigation — Interview Preparation

## 1. Anchor elements

The `<a>` (anchor) element creates a hyperlink. Its `href` attribute specifies the destination:

```html
<a href="https://example.com">Visit the example site</a>
```

- Use an anchor for **navigation** to another page, document, or location.
- Visible link text should describe the destination or action.
- If an anchor has no `href`, it is not a functional hyperlink; use a `<button>` for an action instead.
- A link does not automatically open in a new tab; by default, it navigates in the current browsing context.

## 2. Absolute URLs

An absolute URL specifies the full address of a resource, including its scheme and host:

```html
<a href="https://developer.mozilla.org/en-US/docs/Web/HTML">HTML documentation</a>
```

An absolute URL can also point to a specific location:

```html
<a href="https://example.com/guide#install">Installation guide</a>
```

Use the full URL when linking to an external site or when the complete destination needs to be explicit.

## 3. Relative URLs

A relative URL identifies a destination relative to the current document or the site's configured base URL:

```html
<!-- If the current page is /projects/index.html -->
<a href="about.html">About this project</a>
<a href="../index.html">Project home</a>
<a href="/contact">Contact page from the site root</a>
```

Common patterns:

- `about.html` — a path relative to the current document's directory.
- `../images/scan.png` — move up to a parent directory, then into `images`.
- `/contact` — a path starting at the site's root.
- `#workflow` — a fragment on the current document.

Relative links are useful when the destination belongs to the same site, especially if the site may be deployed under a different domain.

## 4. Internal page links

An internal link navigates to another page or location within the same site:

```html
<a href="/pipeline">Pipeline guide</a>
```

For static projects, an internal link may reference another file:

```html
<a href="pipeline.html">Pipeline guide</a>
```

Use clear link text. Avoid vague labels like “click here” when the destination is not clear from surrounding context.

## 5. External links

An external link navigates to a different website:

```html
<a href="https://example.org/research">Read the research paper</a>
```

- Include the correct URL scheme, usually `https://`.
- Make the destination clear when it may surprise users. For example, identify an external documentation or social-media link.
- Opening an external link in the same tab is a valid default; do not assume every external link should open a new tab.
- Do not use a button for ordinary navigation.

## 6. Open links in new tabs

Set `target="_blank"` to request that a link open in a new browsing context, commonly a new tab:

```html
<a href="https://example.org/research"
   target="_blank"
   rel="noopener">
  Read the research paper (opens in a new tab)
</a>
```

Important details:

- `target="_blank"` asks the browser to open a new context; browser settings may affect the exact behavior.
- Opening a new tab can surprise people, so use it only when it benefits the user and make the behavior clear.
- Add `rel="noopener"` to prevent the new page from accessing the original page through `window.opener`. Modern browsers commonly apply this protection to `_blank`, but stating it explicitly communicates the intent and supports older behavior.
- Use `rel="noreferrer"` only when you also intend to suppress the `Referer` header; it has privacy and analytics implications and is not required in every case.
- Do not use `target="_blank"` without a valid `href`.

## 7. Email links

Use the `mailto:` URL scheme to create a link that can open the user's configured email application:

```html
<a href="mailto:research@example.com">Email the research team</a>
```

You can add optional subject and body parameters:

```html
<a href="mailto:research@example.com?subject=Project%20question">
  Ask a project question
</a>
```

- Spaces and special characters in URL parameters should be percent-encoded.
- A `mailto:` link does not send an email by itself; the user's email client handles it.
- Do not assume every user has a desktop mail application configured.
- An email address can attract spam if published publicly.

## 8. Telephone links

Use the `tel:` URL scheme to make a phone number actionable on devices that support calling:

```html
<a href="tel:+12025550123">Call +1 202 555 0123</a>
```

- Use a clear, internationally formatted number where appropriate.
- The displayed number can include spaces or punctuation for readability.
- `tel:` does not place a call on every device; the operating system or browser decides how to handle it.
- Do not create a telephone link if there is no real number or if contact by phone is not intended.

## 9. Bookmark links (fragment links)

A fragment link, sometimes called a bookmark link, navigates to an element with a matching `id`:

```html
<nav aria-label="On this page">
  <a href="#preprocessing">Preprocessing</a>
</nav>

<section id="preprocessing">
  <h2>Preprocessing</h2>
  <p>Prepare the image before model evaluation.</p>
</section>
```

- The fragment begins with `#`; the target element has the matching `id` without the `#`.
- IDs must be unique within the document.
- To link to a section on another page, combine its URL and fragment: `pipeline.html#preprocessing`.
- Fixed headers can cover the target after navigation. CSS `scroll-margin-top` on target sections can help:

```css
section[id] {
  scroll-margin-top: 5rem;
}
```

- Ensure keyboard users can reach and understand the linked content.

## 10. Navigation menus

Use the `<nav>` landmark for a group of important navigation links. Add an accessible name when a page has more than one navigation area:

```html
<nav aria-label="Main navigation">
  <ul>
    <li><a href="/">Overview</a></li>
    <li><a href="/workspace">Image workspace</a></li>
    <li><a href="/pipeline">Pipeline guide</a></li>
  </ul>
</nav>
```

Good practices:

- Use links inside navigation for destinations; use buttons for actions such as opening a menu or changing a setting.
- Use meaningful link labels that make sense when read out of context.
- Mark the current page where appropriate, for example with `aria-current="page"`:

```html
<a href="/pipeline" aria-current="page">Pipeline guide</a>
```

- Make navigation usable with a keyboard and show a visible focus style.
- On small screens, a menu toggle should be a real `<button>` with an accessible name and its expanded state:

```html
<button type="button" aria-expanded="false" aria-controls="main-menu">
  Open navigation
</button>
<nav id="main-menu" aria-label="Main navigation">
  <!-- Navigation links -->
</nav>
```

- JavaScript should keep `aria-expanded` in sync with whether the menu is open. Do not rely on color alone to indicate the active page.

## Quick comparison

| Link type | Example | Typical purpose |
|---|---|---|
| External absolute URL | `https://example.org/docs` | Visit another website |
| Relative page URL | `guide.html` | Navigate within a static site |
| Root-relative URL | `/contact` | Navigate from the site root |
| Current-page fragment | `#results` | Jump to a section on the current page |
| Other-page fragment | `guide.html#results` | Open another page at a section |
| Email URL | `mailto:team@example.org` | Start composing an email |
| Telephone URL | `tel:+12025550123` | Offer a phone action on supported devices |
| New browsing context | `target="_blank"` | Request that a link open in another tab or window |

## Quick interview review

1. **What element creates a hyperlink?**  
   The `<a>` element. Its `href` attribute supplies the destination.

2. **How do absolute and relative URLs differ?**  
   An absolute URL gives the complete address, while a relative URL resolves from the current document or site root.

3. **How do you link to a section on the same page?**  
   Link to `#section-id` and give the target element the matching, unique `id`.

4. **How do you open a link in a new tab?**  
   Use `target="_blank"` and include `rel="noopener"`; consider clearly telling users that it opens in a new tab.

5. **How do `mailto:` and `tel:` work?**  
   They are URL schemes that ask a supporting application or device to handle the email or phone action; they do not themselves send an email or place a call.

6. **Should a navigation action be a link or a button?**  
   A link navigates to a destination. A button performs an action on the current interface.

7. **How can the current page be communicated accessibly?**  
   Use `aria-current="page"` on the current navigation link.

## Good practices to remember

- Write descriptive link text; avoid using “click here” as the only description.
- Use anchors for navigation and buttons for actions.
- Make IDs unique and match fragment links exactly.
- Use `target="_blank"` thoughtfully and pair it with `rel="noopener"`.
- Give navigation landmarks useful accessible names where needed.
- Ensure menus and links work with the keyboard and have visible focus.
- Remember that `mailto:` and `tel:` depend on user-device handlers.
