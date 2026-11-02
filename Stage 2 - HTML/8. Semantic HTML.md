# HTML Semantic Elements — Interview Preparation

## 1. What is semantic HTML?

Semantic HTML uses elements that describe the **meaning and purpose** of their content. For example, `<nav>` identifies navigation, while `<main>` identifies the page's primary content.

Semantic elements help:

- Browsers and assistive technologies understand a document's structure.
- Users navigate with landmarks and meaningful headings.
- Developers read and maintain the markup.
- Search engines interpret page content.

Semantics do not provide every behavior automatically. A semantic element should still be used with correct structure and accessible labels.

## 2. `<header>`

`<header>` introduces a page or a section. It often contains a heading, logo, introductory content, or navigation:

```html
<header>
  <a href="/">Retina Lab</a>
  <nav aria-label="Main navigation">
    <a href="/overview">Overview</a>
    <a href="/pipeline">Pipeline</a>
  </nav>
</header>
```

- A page may have a site-level header and headers inside individual articles or sections.
- `<header>` is not the same as `<head>`. `<head>` contains document metadata; `<header>` is visible page content.
- A `<header>` must not be a descendant of `<footer>`, `<address>`, or another `<header>`.

## 3. `<footer>`

`<footer>` contains information about its nearest page or section, such as authorship, related links, or copyright:

```html
<footer>
  <p>Research notes for the image-processing project.</p>
  <a href="/contact">Contact</a>
</footer>
```

- A document can have a page-level footer, and articles or other sections can have their own footers.
- Footer content varies by context; it is not limited to copyright notices.
- A `<footer>` is not necessarily a visible bar at the bottom of the screen; CSS controls its appearance and position.

## 4. `<main>`

`<main>` identifies the dominant content of the document:

```html
<main>
  <h1>Image workspace</h1>
  <!-- Primary page content -->
</main>
```

- A page should ordinarily have one visible `<main>` element.
- Site-wide content repeated across pages, such as global navigation, usually does not belong inside `<main>`.
- `<main>` helps assistive-technology users navigate directly to the primary content.

## 5. `<nav>`

`<nav>` represents a significant section of navigation links:

```html
<nav aria-label="Workspace navigation">
  <a href="/overview">Overview</a>
  <a href="/images">Image workspace</a>
  <a href="/pipeline">Pipeline guide</a>
</nav>
```

- Use it for important navigation, not every collection of links.
- A page can contain multiple `<nav>` elements. Give them different accessible names when that helps users distinguish them.
- Navigation destinations should be links; controls that perform an action should generally be buttons.

## 6. `<section>`

`<section>` groups related content into a thematic section, usually with a heading:

```html
<section aria-labelledby="preprocessing-title">
  <h2 id="preprocessing-title">Image preprocessing</h2>
  <p>Review the steps used to prepare the image.</p>
</section>
```

- Think of a section as a thematic part of a document, not a generic styling wrapper.
- A section should usually have a heading that describes its subject.
- Use `<div>` when the content needs a generic wrapper but does not have a meaningful section identity.

## 7. `<article>`

`<article>` represents self-contained content that can make sense independently or be distributed separately:

```html
<article>
  <h2>CLAHE contrast preview</h2>
  <p>A local preview of contrast enhancement for an input image.</p>
  <footer>
    <p>Added to the project notes.</p>
  </footer>
</article>
```

Possible examples include a news story, blog post, forum entry, or standalone project update.

- Articles can be nested when an independent item is related to another article.
- Use `<article>` because the content is independently meaningful, not just because it is a card visually.
- A `<section>` organizes related content; an `<article>` is self-contained content. The two can be nested based on meaning.

## 8. `<aside>`

`<aside>` represents content that is indirectly related to the surrounding content, such as a sidebar, a related link list, or a callout:

```html
<aside aria-labelledby="research-note-title">
  <h2 id="research-note-title">Research note</h2>
  <p>This browser preview is not a clinical assessment.</p>
</aside>
```

- Whether content is an aside depends on its relationship to the surrounding material, not whether CSS places it on the left or right.
- A sidebar that contains essential primary content may not be an aside.

## 9. `<details>` and `<summary>`

`<details>` creates a disclosure widget that users can open and close. `<summary>` provides its visible label:

```html
<details>
  <summary>Show preprocessing notes</summary>
  <p>The preview can use green-channel extraction and contrast enhancement.</p>
</details>
```

- The first `<summary>` child acts as the widget's label.
- Add the Boolean `open` attribute to show the content initially:

```html
<details open>
  <summary>Visible by default</summary>
  <p>This content starts expanded.</p>
</details>
```

- Browsers provide basic keyboard and disclosure behavior.
- Use `<details>` for optional supporting information, not to hide essential instructions or critical information from users.

## 10. `<time>`

`<time>` represents a date, time, or duration. The `datetime` attribute provides a machine-readable value:

```html
<time datetime="2026-11-03">November 3, 2026</time>
<time datetime="PT15M">15 minutes</time>
```

- The visible text can be written in a human-friendly format.
- Use a valid machine-readable value when providing `datetime`.
- A duration such as 15 minutes can be represented using an ISO 8601 duration, such as `PT15M`.
- Do not use `<time>` for text that is not actually a date or time.

## 11. `<address>`

`<address>` provides contact information for the nearest `<article>` or for the document as a whole:

```html
<address>
  Project contact:
  <a href="mailto:research@example.org">research@example.org</a>
</address>
```

- It is for contact information, not a general-purpose wrapper around any postal address-like content.
- The appropriate scope depends on where it appears: it may identify the contact details for an article's author or for the site.
- Browsers often italicize it by default; use CSS to change its presentation when desired.

## 12. Semantic versus non-semantic elements

### Semantic elements

Semantic elements communicate meaning or purpose:

- `<main>` — primary page content.
- `<nav>` — significant navigation.
- `<article>` — self-contained content.
- `<button>` — an action control.
- `<time>` — a date or time.

### Non-semantic elements

`<div>` and `<span>` are generic containers:

- `<div>` is a generic block container.
- `<span>` is a generic inline container.
- They have no specific content meaning by themselves.
- They are useful for grouping elements for CSS or JavaScript when no more appropriate semantic element applies.

```html
<div class="image-toolbar">
  <button type="button">Zoom in</button>
  <span class="zoom-level">100%</span>
</div>
```

Use semantic elements when they accurately describe the content. Do not select an element solely because its default style looks appropriate.

## 13. Choosing appropriate HTML elements

Ask what the content **is** and what it **does**, then choose the element that matches:

| Purpose | Appropriate element |
|---|---|
| Primary document content | `<main>` |
| Significant group of navigation links | `<nav>` |
| Thematic content with a heading | `<section>` |
| Independent, self-contained item | `<article>` |
| Tangentially related supporting content | `<aside>` |
| Introductory content for a page or section | `<header>` |
| Contact information for a page or article | `<address>` |
| Date or time | `<time>` |
| User-triggered action | `<button>` |
| Navigation to a destination | `<a href="...">` |
| Generic wrapper with no specific meaning | `<div>` or `<span>` |

Practical questions:

1. Is this content a destination link or an action? Use `<a>` for navigation and `<button>` for an action.
2. Is this a significant group of navigation destinations? Consider `<nav>`.
3. Is this content a distinct topic with a heading? Consider `<section>`.
4. Can this content stand on its own? Consider `<article>`.
5. Is it only a generic grouping for styling or scripting? Use `<div>` or `<span>`.
6. Would a heading help users understand or navigate this content? Add the appropriate heading.

**Important:** HTML semantics come from the chosen element and its structure—not from CSS classes such as `class="header"` on a `<div>`.

## Quick interview review

1. **How is `<header>` different from `<head>`?**  
   `<head>` contains document metadata and linked resources. `<header>` is visible introductory content for a page or section.

2. **How many `<main>` elements should a page generally have?**  
   Usually one visible primary `<main>` element.

3. **When should you use `<section>` instead of `<div>`?**  
   Use `<section>` for a thematic part of a document, usually with a heading. Use `<div>` as a generic wrapper when there is no more meaningful element.

4. **How do `<article>` and `<section>` differ?**  
   An article is self-contained and can stand independently; a section organizes thematically related content.

5. **Should every sidebar use `<aside>`?**  
   No. An aside contains tangentially related content; visual placement alone does not determine its semantics.

6. **What do `<details>` and `<summary>` provide?**  
   A native disclosure widget and its visible label, with basic browser interaction.

7. **What is `<time datetime="...">` for?**  
   It combines a human-readable date or time with an optional machine-readable value.

8. **When should you use `<address>`?**  
   For contact information for the nearest article or the document, not any arbitrary address-styled content.

9. **What is the difference between semantic and non-semantic elements?**  
   Semantic elements communicate the meaning or purpose of their content; generic elements such as `<div>` and `<span>` do not.

## Good practices to remember

- Choose elements by meaning, not by default appearance or layout position.
- Use landmarks such as `<main>` and `<nav>` to make the page easier to navigate.
- Use headings to describe and organize sections.
- Use `<article>` only for content that is independently meaningful.
- Use `<div>` and `<span>` when no suitable semantic element applies.
- Use buttons for actions and links for destinations.
- Keep accessible names and document structure clear; semantics complement, but do not replace, accessibility testing.
