# HTML Accessibility Basics — Interview Preparation

## 1. Why accessibility matters

Web accessibility means designing and building websites so people with different abilities can use them. This includes people who use screen readers, keyboards, voice input, magnification, captions, or other assistive technologies.

Accessibility matters because it:

- Helps more people use the product, including people with permanent, temporary, or situational disabilities.
- Makes content and interactions more predictable for everyone.
- Improves compatibility with assistive technology and different input methods.
- Is part of building inclusive, usable software and may be required by applicable standards or laws.

Accessibility is not an optional finishing step. Consider it throughout design, content, implementation, and testing. Conformance depends on the whole experience; no single HTML attribute makes a page fully accessible.

## 2. Semantic structure

Use HTML elements according to their meaning. Semantic structure gives browsers and assistive technologies information about the content and its relationships:

```html
<header>
  <a href="/">Retina Lab</a>
  <nav aria-label="Main navigation">
    <a href="/overview">Overview</a>
    <a href="/pipeline">Pipeline</a>
  </nav>
</header>

<main>
  <h1>Image workspace</h1>
  <section aria-labelledby="preparation-title">
    <h2 id="preparation-title">Image preparation</h2>
    <p>Prepare the image before reviewing it.</p>
  </section>
</main>
```

Good practices:

- Use landmarks such as `<header>`, `<nav>`, `<main>`, and `<footer>` appropriately.
- Give each page a clear, descriptive primary heading, usually an `<h1>`.
- Use heading levels to communicate hierarchy, not just to control text size.
- Use lists, tables, buttons, and links for their intended purposes.
- Prefer native semantic HTML to generic elements with custom ARIA roles.

Semantic markup improves accessibility, but content, labels, keyboard behavior, contrast, and testing still matter.

## 3. Alternative text for images

The `alt` attribute provides a text alternative for an image:

```html
<img src="vessel-map.png" alt="Highlighted vessels branching from the center of the image">
```

Choose the alternative based on the image's purpose in context:

- **Informative image:** Describe the information the image contributes.
- **Decorative image:** Use an empty alternative (`alt=""`) so assistive technologies can ignore it.
- **Image-only link:** Describe the destination or action of the link.

```html
<a href="/gallery">
  <img src="gallery-preview.jpg" alt="Open the image gallery">
</a>
```

Avoid:

- Omitting `alt` from meaningful images.
- Repeating nearby text when it communicates the same information.
- Writing a visual inventory of every detail when only one detail matters.
- Using a filename or phrases like “image of” as a default alternative.

An empty `alt` is intentional for decorative images; it is not the same as a missing `alt`.

## 4. Associating labels with form controls

Every form control needs a programmatically determinable name. The usual method is a `<label>`.

### Explicit association

```html
<label for="email">Email address</label>
<input id="email" name="email" type="email">
```

The label's `for` value must match the control's `id`. The `id` connects the label to the control; the `name` is generally the key used when the form submits data.

### Implicit association

```html
<label>
  Email address
  <input name="email" type="email">
</label>
```

Useful related guidance:

- A placeholder is not a substitute for a label: it disappears when the user types.
- Use `<fieldset>` and `<legend>` to name a related group of controls, such as a set of radio buttons; still label each individual option.
- Provide instructions and error messages in text, and associate additional help with a control using `aria-describedby` when appropriate.

```html
<label for="sample-code">Sample code</label>
<input id="sample-code" name="sampleCode" aria-describedby="sample-help">
<small id="sample-help">Use two letters, a hyphen, and four digits.</small>
```

## 5. Keyboard navigation

Some users navigate without a mouse. Interactive features must be available using the keyboard.

Typical keyboard interactions include:

- `Tab` and `Shift` + `Tab` to move between focusable controls.
- `Enter` to activate a focused link or button.
- `Space` to activate a button or toggle a checkbox.
- Arrow keys for particular native controls, such as radio groups or select menus.
- `Escape` to dismiss many dialogs and menus when that behavior is provided.

Prefer native HTML controls:

```html
<a href="/pipeline">Read the pipeline</a>
<button type="button">Open image workspace</button>
```

A clickable `<div>` does not automatically behave like a button. It does not inherently receive keyboard focus or provide standard keyboard activation. If a custom control is unavoidable, its focus behavior, role, accessible name, keyboard interactions, and state must be implemented and tested.

Do not remove the browser's focus indicator unless you replace it with an equally visible indicator.

## 6. Focus order

Focus order is the sequence keyboard users follow when moving through interactive elements. It should normally follow the visual and logical reading order of the page.

Good practices:

- Keep DOM order meaningful. CSS visual reordering does not necessarily change keyboard or screen-reader reading order.
- Avoid positive `tabindex` values such as `tabindex="1"`; they can create confusing sequences.
- Use `tabindex="0"` only when a non-interactive element genuinely needs to be added to the normal tab sequence, such as a labelled scrollable region.
- Use `tabindex="-1"` when an element should be focusable by script, but not reached through ordinary Tab navigation.
- When a dialog opens, move focus into it appropriately; when it closes, return focus to the control that opened it.
- Ensure focus is not hidden behind fixed headers, overlays, or sticky controls.

Test by navigating with only the keyboard and checking that the current focused item is always easy to locate.

## 7. Accessible forms

An accessible form lets users understand what information is expected, enter it, and identify and correct errors.

Checklist:

- Provide a visible label for every input, select, and textarea.
- Explain the expected format and indicate required fields in text.
- Use input types that match the data, such as `email` for email addresses.
- Group related checkboxes and radio buttons with `<fieldset>` and `<legend>`.
- Make error messages specific and associate them with the relevant field.
- Do not communicate errors only through color.
- Preserve user-entered values after validation errors where appropriate.
- Make custom validation messages readable to assistive technology.
- Validate on the server as well as in the browser; client-side validation can be bypassed.

Example:

```html
<form action="/contact" method="post">
  <label for="contact-email">Email address</label>
  <input
    id="contact-email"
    name="email"
    type="email"
    autocomplete="email"
    required
    aria-describedby="email-help">
  <small id="email-help">Use an address where we can reach you.</small>

  <button type="submit">Send message</button>
</form>
```

When an error occurs, make the problem clear. For more complex forms, an error summary at the top can link to the fields that need attention.

## 8. ARIA fundamentals

**ARIA** (Accessible Rich Internet Applications) provides attributes that can communicate roles, names, descriptions, states, and relationships to assistive technologies. It does not automatically add visual styling, keyboard behavior, or application logic.

Examples:

- `aria-label`: gives an element an accessible name when visible text is not available or is insufficient.
- `aria-labelledby`: uses another element's text as the accessible name.
- `aria-describedby`: associates descriptive or instructional text.
- `aria-expanded`: reports whether a control's associated content is expanded.
- `aria-current`: identifies the current item in a set, such as the current navigation page.
- `role`: identifies the role of an element when native HTML does not provide the needed semantics.

Example of a disclosure button:

```html
<button type="button" aria-expanded="false" aria-controls="help-panel">
  Show help
</button>
<div id="help-panel" hidden>
  <p>Choose an image to begin.</p>
</div>
```

When the button opens the panel, JavaScript must update `aria-expanded` to `"true"` and reveal the panel; when it closes the panel, update the state and hide it.

Important principles:

- **Use native HTML first.** A `<button>` is usually better than a `<div role="button">`.
- ARIA changes what assistive technologies are told; it does not make an element function like the role you assign.
- Keep ARIA states synchronized with the interface's actual state.
- Do not add a role or ARIA attribute when native HTML already provides the correct semantics.
- Incorrect ARIA can make the experience worse. Test with keyboard and assistive technologies.

## 9. Accessible button names

Every button should have an accessible name that explains its purpose:

### Visible text

```html
<button type="button">Remove selected image</button>
```

Visible text is the simplest and most robust button name.

### Icon-only button

If a button contains only an icon, provide a programmatic name:

```html
<button type="button" aria-label="Close dialog">
  <svg aria-hidden="true" viewBox="0 0 20 20">
    <path d="m5 5 10 10M15 5 5 15"></path>
  </svg>
</button>
```

- `aria-label` supplies the name, and `aria-hidden="true"` prevents the decorative icon from being announced as redundant content.
- Give repeated controls distinct, contextual names when needed, such as “Remove retinal image” rather than just “Remove.”
- An `aria-label` does not replace a visible label where users need visible instructions.
- Do not make the accessible name misleading or contradictory to the visible text.

## Common interview pitfalls

- **A semantic element is not automatically a fully accessible experience.** Interaction, content, and states still matter.
- **ARIA does not implement keyboard behavior.** A custom button still needs keyboard support and correct state handling.
- **A placeholder is not a label.**
- **Use `alt=""` for decorative images; do not omit `alt` on meaningful images.**
- **Do not remove focus outlines without providing an equally visible alternative.**
- **The visual order and the DOM order can differ; verify that keyboard order remains understandable.**
- **Avoid positive `tabindex` values.**
- **An icon-only button needs an accessible name.**
- **Client-side form validation does not replace server-side validation.**

## Quick interview review

1. **Why use semantic HTML?**  
   It communicates structure and purpose to browsers, assistive technologies, and developers, improving navigation and maintainability.

2. **How do you choose `alt` text?**  
   Describe the information the image contributes in context; use `alt=""` when the image is purely decorative.

3. **How do you connect a label to a form field?**  
   Match `<label for="field-id">` to the control's `id`, or wrap the control inside its label.

4. **What makes a control keyboard-accessible?**  
   It can be reached and operated using the keyboard with an understandable focus order and visible focus. Native controls provide much of this behavior by default.

5. **What is ARIA for?**  
   Communicating accessible roles, names, descriptions, states, and relationships when native HTML is not enough; ARIA does not add behavior by itself.

6. **How do you name an icon-only button?**  
   Give the button visible text or an appropriate accessible name, commonly using `aria-label`, and hide a decorative icon from assistive technology.

7. **What is a good focus order?**  
   A sequence that follows the page's logical reading and interaction order and keeps the focused item visible.

8. **Does a website become accessible just by adding ARIA?**  
   No. Semantic markup, keyboard support, clear content, visible focus, accessible forms, appropriate contrast, and testing are all important.

## Practical accessibility review

Before delivery, try the interface without a mouse:

1. Use Tab and Shift+Tab to reach every interactive control.
2. Check that focus is visible and follows a sensible order.
3. Activate links and buttons with their expected keyboard controls.
4. Check that icon-only buttons have clear names.
5. Inspect image alternatives and decorative images.
6. Check that labels, instructions, and form errors are associated with fields.
7. Review headings and landmarks for a useful document structure.
8. Test with a screen reader and automated tools as part of a broader accessibility review; automated checks alone cannot confirm usability.
