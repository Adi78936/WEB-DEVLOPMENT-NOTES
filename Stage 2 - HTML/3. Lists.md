# HTML Lists — Interview Preparation

## 1. Ordered lists: `<ol>`

Use an ordered list when the sequence or ranking of items matters. Each list item is marked with `<li>`:

```html
<ol>
  <li>Select an image.</li>
  <li>Prepare the image.</li>
  <li>Review the preview.</li>
</ol>
```

By default, browsers number the items. You can change the numbering with attributes:

```html
<ol start="3">
  <li>Third step</li>
  <li>Fourth step</li>
</ol>

<ol reversed>
  <li>Newest entry</li>
  <li>Earlier entry</li>
</ol>

<ol type="A">
  <li>First option</li>
  <li>Second option</li>
</ol>
```

- `start` sets the starting number.
- `reversed` requests descending numbering.
- `type` selects a marker style, such as `1`, `A`, `a`, `I`, or `i`.
- CSS is generally preferred for presentation-only marker styling.

## 2. Unordered lists: `<ul>`

Use an unordered list when items form a group but their sequence is not important:

```html
<ul>
  <li>JPEG images</li>
  <li>PNG images</li>
  <li>WEBP images</li>
</ul>
```

Browsers commonly display bullets by default. Change marker appearance with CSS rather than choosing a list type based on its visual marker.

## 3. List items: `<li>`

`<li>` represents an item in an ordered or unordered list. It should normally be a child of `<ol>` or `<ul>`. A list item can contain text, links, or other flow content, including a nested list.

```html
<ul>
  <li><a href="/pipeline">Pipeline guide</a></li>
</ul>
```

Do not use list elements only to create indentation or layout; choose them when the content is semantically a list.

## 4. Description lists: `<dl>`, `<dt>`, and `<dd>`

A description list associates terms with their descriptions or values:

```html
<dl>
  <dt>CLAHE</dt>
  <dd>Contrast Limited Adaptive Histogram Equalization.</dd>

  <dt>CNN</dt>
  <dd>Convolutional neural network.</dd>
</dl>
```

- `<dl>` contains the description-list groups.
- `<dt>` represents a term or name.
- `<dd>` provides its description or value.
- A term may have more than one description, and a description may correspond to more than one term.

Description lists are useful for glossaries, metadata, and term-value content. They are not only for dictionary definitions.

## 5. Nested lists

A nested list is a list inside a list item. It represents a hierarchy, such as categories with subcategories:

```html
<ul>
  <li>Image preparation
    <ol>
      <li>Extract the green channel</li>
      <li>Improve local contrast</li>
    </ol>
  </li>
  <li>Model evaluation</li>
</ul>
```

The inner `<ol>` belongs inside the parent `<li>`. Nesting a list directly under another `<ul>` or `<ol>`, without an intervening `<li>`, is invalid structure.

Use nesting only when the content has a meaningful parent-child relationship. Avoid unnecessary deep nesting, which can be difficult to scan and navigate.

## 6. Navigation lists

Navigation is a group of links to destinations. It can be represented with a `<nav>` landmark and a list of links:

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

- `<nav>` identifies a significant group of navigation links. It can contain a list, but a `<ul>` is not required in every navigation design.
- Give each `<nav>` a descriptive accessible name when a page has multiple navigation landmarks, for example `aria-label="Main navigation"` and `aria-label="On this page"`.
- Use `<a href="...">` for navigation destinations. Use a `<button>` for an action such as opening a menu or changing a setting.
- Mark the current destination where appropriate:

```html
<li><a href="/pipeline" aria-current="page">Pipeline guide</a></li>
```

- Keep link names clear, and ensure the navigation is keyboard-accessible with a visible focus style.
- Use CSS to control layout and list-marker appearance; do not remove list semantics just to change how the list looks.

## 7. Styling list markers

CSS controls the appearance and position of list markers:

```css
.feature-list {
  list-style-type: square;
  padding-inline-start: 1.25rem;
}

.navigation-list {
  display: flex;
  gap: 1rem;
  padding: 0;
  list-style: none;
}
```

Common `list-style-type` values include `disc`, `circle`, `square`, `decimal`, and `lower-roman`. A navigation list often hides visual markers, but it should remain a list when the content is genuinely a group of related navigation items.

## Quick comparison

| Element | Purpose |
|---|---|
| `<ol>` | Items whose sequence or ranking matters |
| `<ul>` | A group of items whose sequence is not significant |
| `<li>` | An item in an ordered or unordered list |
| `<dl>` | Terms and associated descriptions or values |
| `<dt>` | A term or name in a description list |
| `<dd>` | A description or value associated with a term |
| `<nav>` | A significant group of navigation links |

## Quick interview review

1. **When should you use `<ol>` instead of `<ul>`?**  
   Use `<ol>` when the order or ranking of the items matters; use `<ul>` when it does not.

2. **What elements make up a description list?**  
   `<dl>` contains one or more `<dt>` term and `<dd>` description/value groups.

3. **Where should a nested list go?**  
   Inside the `<li>` that owns the nested items.

4. **Does navigation always need a list?**  
   No. A `<nav>` landmark identifies navigation; a `<ul>` is a common semantic way to group multiple links, but it is not mandatory for every design.

5. **How should you mark the current navigation page?**  
   Use `aria-current="page"` on the link representing the current page.

6. **Should lists be used to lay out columns or indent text?**  
   No. Use CSS layout for visual arrangement, and lists for content that is semantically a group of items.

## Good practices to remember

- Choose ordered or unordered lists by meaning, not by the marker they display.
- Put list items inside `<ol>` or `<ul>`, and put nested lists inside the appropriate parent `<li>`.
- Use description lists for associated terms and values.
- Use `<nav>` to identify significant navigation regions; provide clear link labels.
- Keep nested structures understandable, and style lists with CSS.
