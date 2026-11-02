# HTML Text and Formatting — Interview Preparation

## 1. Heading elements: `<h1>` to `<h6>`

HTML provides six heading levels. `<h1>` is the highest-level heading, and `<h6>` is the lowest.

```html
<h1>Retinal Image Research</h1>
<h2>Image preparation</h2>
<h3>Contrast enhancement</h3>
```

- Choose a heading level based on the content hierarchy, not its default font size.
- Use CSS to change how a heading looks.
- Keep the hierarchy logical: a section heading should be nested conceptually beneath its parent heading.
- Headings help people scan a page and help assistive technologies navigate its sections.
- A page may contain more than one `<h1>` in modern HTML, but a clear, predictable heading outline is generally easier to understand.

**Interview distinction:** Headings communicate document structure; they are not simply large or bold text.

## 2. Paragraph: `<p>`

The `<p>` element represents a paragraph of text:

```html
<p>Images are prepared locally before model evaluation.</p>
```

Browsers display paragraphs as blocks by default and add spacing around them. Do not use `<p>` just to add vertical space; use CSS for spacing.

## 3. Line breaks: `<br>`

`<br>` creates a line break within text, without starting a new paragraph:

```html
<p>Research Lab<br>Image Processing Group</p>
```

- `<br>` is a void element and has no closing tag.
- Use it where a line break is part of the content, such as a postal address or a poem.
- Do not use repeated `<br>` elements to create layout spacing; use CSS margins, padding, or layout rules.

## 4. Horizontal rule: `<hr>`

`<hr>` represents a thematic break between sections or topics. It is not merely a decorative line:

```html
<p>Image acquisition is complete.</p>
<hr>
<p>Next, the image can be preprocessed.</p>
```

`<hr>` is a void element. Its appearance can be styled with CSS.

**Interview distinction:** `<br>` separates lines within text; `<hr>` signals a thematic change in content.

## 5. Bold and strong: `<b>` and `<strong>`

Both elements commonly appear bold in browsers, but they have different meaning:

- `<strong>` marks content with strong importance, seriousness, or urgency.
- `<b>` draws attention to text without adding importance, such as a keyword or product name.

```html
<p><strong>Important:</strong> This prototype does not provide a diagnosis.</p>
<p>Search for the <b>green channel</b> step in the pipeline.</p>
```

For styling alone, use CSS rather than choosing an element based on its default bold appearance.

## 6. Italic and emphasis: `<i>` and `<em>`

Both elements commonly appear italic by default, but their semantics differ:

- `<em>` adds stress emphasis. Nested `<em>` elements can indicate stronger emphasis.
- `<i>` identifies text in an alternate voice or mood, or a term that is conventionally italicized, such as a technical term or taxonomic name.

```html
<p>Please <em>do not</em> use an unvalidated prediction for clinical decisions.</p>
<p>The term <i>fundus</i> refers to the interior surface of the eye.</p>
```

Use CSS for italics that are purely visual and carry no semantic meaning.

## 7. Underline: `<u>`

`<u>` marks text with a non-textual annotation, such as a misspelled word or a proper name in some writing systems:

```html
<p>The draft contains a <u>misspelled</u> label.</p>
```

- It commonly appears underlined by default.
- Do not use `<u>` as a substitute for an unvisited link; underlining is commonly associated with links.
- If an underline is purely decorative, use CSS such as `text-decoration: underline`.

## 8. Superscript and subscript: `<sup>` and `<sub>`

- `<sup>` displays content as superscript.
- `<sub>` displays content as subscript.

Use these when the position is meaningful, such as exponents, footnote markers, or chemical formulas:

```html
<p>Area is measured in pixels squared: px<sup>2</sup>.</p>
<p>Water has the chemical formula H<sub>2</sub>O.</p>
```

Do not use these elements just to make text smaller or shift it for visual styling.

## 9. Preformatted text: `<pre>`

`<pre>` represents a block of preformatted text. Browsers preserve its whitespace and line breaks. It is often paired with `<code>` for code examples:

```html
<pre><code>const channel = "green";
preparePreview(channel);</code></pre>
```

- Whitespace inside `<pre>` is meaningful and displayed as written.
- Long lines may need CSS such as `overflow-x: auto` to avoid breaking a layout.
- Use `<pre>` for content where whitespace and line breaks are significant, not to create general-purpose spacing.

## 10. Code and keyboard input: `<code>` and `<kbd>`

### `<code>`

Represents a fragment of computer code:

```html
<p>Use <code>document.querySelector()</code> to find an element.</p>
```

Use `<code>` for code fragments; use `<pre><code>...</code></pre>` for a multiline code block.

### `<kbd>`

Represents user input, commonly keyboard input:

```html
<p>Open developer tools with <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>I</kbd>.</p>
```

Browsers often display these elements in a monospace font, but their purpose is semantic, not just visual.

## 11. Blockquotes: `<blockquote>`

`<blockquote>` represents a quotation taken from another source. It is typically used for longer, block-level quotations:

```html
<blockquote cite="https://example.com/research">
  <p>Reproducible evaluation requires a clearly described methodology.</p>
</blockquote>
```

- The optional `cite` attribute can identify the source URL; it is not necessarily shown to the reader.
- Include visible attribution in the page when appropriate.
- Use `<q>` for a short, inline quotation.
- Do not use `<blockquote>` only to indent text; use CSS for layout.

## 12. Abbreviations: `<abbr>`

`<abbr>` identifies an abbreviation or acronym. The `title` attribute can provide its expanded form:

```html
<p><abbr title="Contrast Limited Adaptive Histogram Equalization">CLAHE</abbr>
improves local contrast.</p>
```

- The abbreviation remains the visible text.
- The `title` attribute may provide an expansion, though its support and discoverability vary across browsers and assistive technologies.
- For an important or first-use definition, consider also writing the expansion directly in the text:

```html
<p>Contrast Limited Adaptive Histogram Equalization (CLAHE) improves local contrast.</p>
```

## Quick comparison

| Purpose | Element | Meaning |
|---|---|---|
| Main or section heading | `<h1>`–`<h6>` | Heading hierarchy |
| Paragraph | `<p>` | Paragraph of text |
| Line break | `<br>` | Break within a line-based piece of text |
| Thematic break | `<hr>` | Change of topic or section |
| Strong importance | `<strong>` | Important content |
| Attention without importance | `<b>` | Stylistic attention |
| Stress emphasis | `<em>` | Emphasized words |
| Alternate voice or term | `<i>` | Text in an alternate voice or mood |
| Annotated text | `<u>` | Non-textual annotation |
| Superscript / subscript | `<sup>` / `<sub>` | Meaningful raised or lowered text |
| Whitespace-sensitive text | `<pre>` | Preformatted block |
| Code | `<code>` | Code fragment |
| Keyboard input | `<kbd>` | User-entered input |
| Longer quotation | `<blockquote>` | Block quotation |
| Abbreviation | `<abbr>` | Abbreviation or acronym |

## Quick interview review

1. **What is the difference between `<strong>` and `<b>`?**  
   `<strong>` conveys importance; `<b>` draws attention without asserting importance.

2. **What is the difference between `<em>` and `<i>`?**  
   `<em>` conveys stress emphasis; `<i>` marks an alternate voice, mood, or conventionally italicized term.

3. **When should you use `<br>`?**  
   For a meaningful line break within content, such as an address—not to create spacing.

4. **What does `<hr>` represent?**  
   A thematic change or separation between topics, not merely a decorative horizontal line.

5. **How do you mark up a code example?**  
   Use `<code>` for code, and wrap a multiline preformatted block in `<pre><code>...</code></pre>`.

6. **When should `<sup>` and `<sub>` be used?**  
   When superscript or subscript positioning is part of the content's meaning, as in exponents or chemical formulas.

7. **How is a quotation different from emphasis?**  
   Use `<blockquote>` for a quotation from another source; use `<em>` to stress a word or phrase.

## Good practices to remember

- Choose text elements for their meaning; use CSS for appearance and spacing.
- Use a logical heading hierarchy to make long documents easier to navigate.
- Prefer `<strong>` and `<em>` when the text truly conveys importance or emphasis.
- Use `<br>` and `<hr>` only for their respective content meanings.
- Mark code, keyboard input, quotations, and abbreviations with their semantic elements.
- Include context or attribution for quotations and expand unfamiliar abbreviations for readers.
