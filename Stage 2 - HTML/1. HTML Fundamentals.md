# HTML Fundamentals — Interview Preparation

## 1. What is HTML?

**HTML** (HyperText Markup Language) is the standard markup language used to structure content on the web. It describes the meaning and organization of content—such as headings, paragraphs, links, images, and forms.

HTML is **not a programming language**: it does not provide general-purpose logic or computation. Browsers parse HTML into a document tree called the **DOM** (Document Object Model), which CSS can style and JavaScript can interact with.

**Interview answer:** HTML gives web content its structure and meaning; CSS controls its presentation, and JavaScript adds behavior.

## 2. HTML document structure

A typical HTML document has a doctype declaration, a root `html` element, document metadata inside `head`, and visible page content inside `body`.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>My page</title>
  </head>
  <body>
    <h1>Page heading</h1>
    <p>Visible page content.</p>
  </body>
</html>
```

### `<!DOCTYPE html>`

- Declares that the document uses modern HTML (HTML5).
- It is a declaration, not an HTML element or tag.
- Place it at the beginning of the document.
- It helps the browser render the page in standards mode rather than quirks mode.

### `<html>`

- The root element containing the entire HTML document.
- Its `lang` attribute identifies the primary language of the page, for example `lang="en"`.
- Declaring the language helps assistive technologies and language-aware tools.

### `<head>`

Contains document metadata and linked resources. Its contents are generally not displayed as page content.

Common contents include:

- `<title>`: the document title shown in the browser tab and commonly used in search results.
- `<meta charset="UTF-8">`: declares the character encoding.
- `<meta name="viewport" ...>`: helps the page use the device's viewport on mobile.
- `<meta name="description" ...>`: provides a page summary for search and sharing contexts.
- `<link>`: connects external resources, such as stylesheets or icons.
- `<script>`: loads or contains JavaScript; scripts can also be placed elsewhere as appropriate.

### `<body>`

Contains the document content presented to users, such as headings, paragraphs, images, navigation, and forms. A document has one `body` element.

## 3. HTML elements and tags

An **HTML element** is a complete unit of markup. It usually consists of an opening tag, content, and a closing tag:

```html
<p>This paragraph is an element.</p>
```

- `<p>` is the opening tag.
- `</p>` is the closing tag.
- The text between them is the content.
- Together, these form the paragraph element.

A **tag** is the markup notation written inside angle brackets. In conversation, people sometimes use “tag” and “element” interchangeably, but they are not exactly the same: tags mark an element's boundaries; the element includes its content and tags.

Some elements are **void elements**: they do not have content or a closing tag. Examples include:

```html
<img src="retina.png" alt="Retinal scan">
<br>
<meta charset="UTF-8">
```

Do not write a separate closing tag for a void element.

## 4. HTML attributes

Attributes provide additional information or configuration for an element. They are written in the opening tag, usually as a name and a value:

```html
<a href="https://example.com" target="_blank" rel="noopener">
  Visit the site
</a>
```

- `href`, `target`, and `rel` are attribute names.
- Values are commonly quoted.
- Some attributes are **Boolean attributes**: their presence enables the setting. For example, `<input disabled>` is disabled; `disabled="false"` still means the attribute is present.

Common examples:

- `href`: link destination.
- `src`: resource location, such as an image source.
- `alt`: text alternative for an image.
- `id`: unique identifier within the document.
- `class`: one or more names used to group elements for styling or scripting.
- `lang`: language of an element or document.
- `title`: advisory information, often exposed as a tooltip.

Use the attribute that expresses the intended meaning. For example, use a link (`<a href="...">`) for navigation and a button (`<button>`) for an action.

## 5. Nested elements

An element is **nested** when it appears inside another element:

```html
<p>Read the <strong>important</strong> note.</p>
```

`<strong>` is nested inside `<p>`. Elements must be closed in the reverse order in which they were opened. This is valid:

```html
<p><strong>Important text</strong></p>
```

This is invalid because the elements overlap rather than nest correctly:

```html
<p><strong>Important text</p></strong>
```

Valid nesting matters because browsers build the DOM from the document markup. Invalid structure can cause browsers to repair the markup in unexpected ways.

## 6. Parent and child elements

In the DOM tree, an element directly containing another element is its **parent**; the contained element is its **child**:

```html
<ul>
  <li>First item</li>
  <li>Second item</li>
</ul>
```

- `<ul>` is the parent of both `<li>` elements.
- Each `<li>` is a child of `<ul>`.
- The two `<li>` elements are siblings.
- An element inside a child, but not directly inside the original element, is a descendant.

Knowing these relationships helps when structuring content, applying CSS selectors, and working with the DOM in JavaScript.

## 7. Block-level and inline elements

These terms describe common layout behavior, especially in the CSS **normal flow**:

- **Block-level behavior:** an element typically starts on a new line and takes the available width by default. Examples include `<div>`, `<p>`, and headings such as `<h1>`.
- **Inline behavior:** an element typically flows within a line of text and takes only the space its content needs. Examples include `<span>`, `<a>`, and `<strong>`.

```html
<p>A paragraph is block-level by default.</p>
<p>A link such as <a href="/about">About</a> flows inline.</p>
```

**Important:** “block” and “inline” do not determine an element's meaning. They describe its typical default display behavior. CSS can change that behavior with the `display` property. Prefer semantic HTML elements whose meaning fits the content; choose layout with CSS.

## 8. HTML comments

Comments are notes in the source that the browser does not display as page content:

```html
<!-- Explain a non-obvious section of markup here. -->
```

- Comments begin with `<!--` and end with `-->`.
- Avoid putting passwords, private data, or sensitive implementation details in comments: source files can be viewed by users.
- HTML comments cannot be nested reliably; avoid trying to place one comment inside another.

## 9. HTML entities

Some characters have special meaning in HTML markup. **Character references** (often called HTML entities) let you write those characters as text.

Common named references:

| Character | Reference |
|---|---|
| `<` | `&lt;` |
| `>` | `&gt;` |
| `&` | `&amp;` |
| `"` | `&quot;` |
| `'` | `&apos;` |
| Non-breaking space | `&nbsp;` |

Example:

```html
<p>Use &lt;strong&gt; to mark strong importance.</p>
<p>Research &amp; development</p>
```

Numeric character references are also available, such as `&#169;` or `&#x00A9;` for `©`. Use UTF-8 for ordinary text; entities are mainly useful when a character would otherwise be interpreted as markup or when a particular character reference is needed.

## Quick interview review

1. **What does HTML do?**  
   It describes the structure and meaning of web content; browsers parse it into the DOM.

2. **Is `<!DOCTYPE html>` an HTML tag?**  
   No. It is a document-type declaration that signals modern HTML and helps the browser use standards mode.

3. **What is the difference between a tag and an element?**  
   A tag is the markup notation; an element is the complete construct, including its tags and content where applicable.

4. **What is a void element?**  
   An element that cannot contain content and has no closing tag, such as `<img>` or `<meta>`.

5. **How do `head` and `body` differ?**  
   `head` contains document metadata and linked resources; `body` contains the page's visible content.

6. **What is the difference between a parent and a descendant?**  
   A parent directly contains a child; a descendant can be nested at any depth inside an element.

7. **Are block and inline properties fixed?**  
   They describe typical default display behavior. CSS can change the display behavior.

8. **Why escape `<` and `&` in text?**  
   They have special meaning in HTML syntax; character references such as `&lt;` and `&amp;` represent them as text.

## Good practices to remember

- Start with `<!DOCTYPE html>` and specify the document language.
- Use semantic elements and valid nesting.
- Quote attribute values for readability and consistency.
- Provide useful `alt` text for meaningful images; use an empty `alt=""` for decorative images.
- Use `id` for a unique element identifier and `class` for reusable groups.
- Use links for navigation and buttons for actions.
- Keep comments helpful and free of sensitive information.
