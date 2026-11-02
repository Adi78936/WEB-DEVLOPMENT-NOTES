# HTML Forms — Interview Preparation

Forms let users submit information or request an action. A reliable form has a clear submission destination, correctly named controls, accessible labels, and appropriate validation.

## 1. The `<form>` element

`<form>` groups interactive controls that submit data:

```html
<form action="/contact" method="post">
  <!-- Labeled form controls -->
  <button type="submit">Send message</button>
</form>
```

Important behavior:

- A submit button inside a form submits that form by default.
- For a control's value to be included in the submitted data, it normally needs a `name`.
- Successful controls are generally enabled, named controls that participate in submission. Unchecked checkboxes and radio buttons are not submitted.
- HTML validation can stop a form from submitting until its constraints are satisfied.
- Client-side validation is useful feedback, but it does not replace server-side validation.

## 2. Form destination: `action`

The `action` attribute specifies the URL that receives a form submission:

```html
<form action="/search" method="get">
  ...
</form>
```

If `action` is omitted, the form submits to the current document URL. The browser sends the form data to the destination; the server or application must actually implement the endpoint for the submission to have a useful result.

## 3. GET and POST methods

The `method` attribute controls how the form data is submitted.

### GET

```html
<form action="/search" method="get">
  <label for="query">Search</label>
  <input id="query" name="q" type="search">
  <button type="submit">Search</button>
</form>
```

- Values are generally appended to the URL as a query string, such as `/search?q=retina`.
- Appropriate for retrieving data and submitting searches or filters.
- A URL can be bookmarked, shared, or refreshed with the same query.
- Do not use GET for sensitive information: query values can appear in browser history, logs, copied links, and other places.
- GET requests are intended to retrieve resources, not make a state-changing operation.

### POST

```html
<form action="/contact" method="post">
  ...
</form>
```

- Form data is sent in the request body rather than appended as query parameters.
- Commonly used for operations that submit data or change server state.
- POST does not, by itself, encrypt information or make it secure. Use HTTPS and appropriate server-side protections.
- A server endpoint must be implemented to receive and handle the request.

**Interview answer:** Use GET for retrieval and searchable/bookmarkable parameters; use POST for submissions that create or change data. The choice is about request semantics, not just hiding values from the URL.

## 4. The `<input>` element

`<input>` creates a form control. The `type` attribute selects its behavior:

```html
<label for="name">Name</label>
<input id="name" name="name" type="text">
```

`<input>` is a void element. Choose a suitable `type`, give the control an accessible label, and set its `name` when its value should be submitted.

## 5. Text input

Use `type="text"` for a single-line text value:

```html
<label for="full-name">Full name</label>
<input id="full-name" name="fullName" type="text" autocomplete="name">
```

Useful attributes include `minlength`, `maxlength`, `autocomplete`, and `required`.

## 6. Email input

Use `type="email"` for an email address:

```html
<label for="email">Email address</label>
<input id="email" name="email" type="email" autocomplete="email" required>
```

- Browsers can check that the value follows a basic email-address format.
- They may offer an email-friendly keyboard on mobile devices.
- A browser's format check cannot confirm that the address exists or that the user owns it.
- Validate and verify important addresses on the server as well.

## 7. Password input

Use `type="password"` to mask text as it is entered:

```html
<label for="password">Password</label>
<input
  id="password"
  name="password"
  type="password"
  autocomplete="new-password"
  required>
```

- Masking helps obscure the value on screen; it does **not** encrypt the value or provide security on its own.
- Use HTTPS for transmission and handle credentials securely on the server.
- For sign-in, `autocomplete="current-password"` may be appropriate; for account creation, use `autocomplete="new-password"`.
- Do not prevent password managers from working without a strong reason.

## 8. Number input

Use `type="number"` for a numeric value where the browser's numeric controls and validation make sense:

```html
<label for="sample-count">Number of samples</label>
<input id="sample-count" name="sampleCount" type="number" min="1" max="100" step="1">
```

- `min`, `max`, and `step` can constrain the allowed range or increments.
- Number controls may include spinner buttons.
- For identifiers that contain digits but are not quantities—such as postal codes or account numbers—use text input with an appropriate `inputmode`, not `type="number"`.

## 9. Date input

Use `type="date"` for a calendar date:

```html
<label for="study-date">Study date</label>
<input id="study-date" name="studyDate" type="date">
```

- The displayed date picker varies by browser and operating system.
- The submitted value is normally normalized as `YYYY-MM-DD`.
- Use `min` and `max` to constrain an allowed date range.
- Do not assume the visual format is identical across devices.

## 10. Checkboxes

Checkboxes allow independent, optional selections. A user can select none, one, or several:

```html
<fieldset>
  <legend>Optional preprocessing</legend>
  <label>
    <input type="checkbox" name="preprocessing" value="clahe">
    Apply contrast enhancement
  </label>
  <label>
    <input type="checkbox" name="preprocessing" value="denoise">
    Apply denoising
  </label>
</fieldset>
```

- An unchecked checkbox is not normally included in submitted form data.
- A checked checkbox submits its `value`; if `value` is omitted, the default submitted value is commonly `"on"`.
- Use checkboxes when options can be selected independently.

## 11. Radio buttons

Radio buttons allow one choice from a group:

```html
<fieldset>
  <legend>Image source</legend>
  <label><input type="radio" name="source" value="upload" required> Upload</label>
  <label><input type="radio" name="source" value="sample"> Use a sample</label>
</fieldset>
```

- Radio buttons belong to the same group when they share the same `name`.
- Only one value in a group can be selected at a time.
- Give each option its own label and use `<fieldset>` and `<legend>` to name the group.
- Use radio buttons for mutually exclusive choices and checkboxes for independent choices.

## 12. Submit and reset buttons

### Submit

```html
<button type="submit">Save changes</button>
```

Submitting triggers form submission and built-in constraint validation unless validation has deliberately been disabled.

`<input type="submit" value="Save changes">` can also submit a form, but `<button>` is often more flexible because it can contain richer content.

### Reset

```html
<button type="reset">Reset form</button>
```

A reset button restores controls to their initial values. It does not submit the form.

- Reset can erase the user's work unexpectedly, so include it only when resetting is genuinely useful.
- Provide clear labels so its effect is understood.

### Explicit button types

An untyped `<button>` inside a form defaults to submitting the form. Make the intended behavior explicit:

```html
<button type="submit">Submit</button>
<button type="button">Preview</button>
<button type="reset">Reset</button>
```

## 13. Select and option

`<select>` presents a menu of choices; `<option>` represents a choice:

```html
<label for="severity">Choose a study category</label>
<select id="severity" name="severity" required>
  <option value="">Select a category</option>
  <option value="0">No DR</option>
  <option value="1">Mild DR</option>
  <option value="2">Moderate DR</option>
</select>
```

- A `<label>` should identify the select.
- The submitted value comes from an option's `value`; if omitted, the option's text is used.
- A placeholder-like option can use `value=""` with `required`, so choosing it does not satisfy the required selection.
- Use `<optgroup label="...">` to group related options.
- Add `multiple` only when selecting several values is a genuine requirement.

## 14. Textarea

`<textarea>` accepts multi-line text:

```html
<label for="notes">Research notes</label>
<textarea id="notes" name="notes" rows="5" maxlength="2000"></textarea>
```

- Unlike `<input>`, `<textarea>` has opening and closing tags.
- Initial text, if any, belongs between the tags.
- `rows`, `cols`, `minlength`, `maxlength`, and `required` can affect its dimensions or constraints.
- Use CSS for responsive sizing.

## 15. Labels

Labels give controls an accessible name and increase the clickable area.

### Explicit label

Connect a label's `for` attribute to the control's unique `id`:

```html
<label for="email">Email address</label>
<input id="email" name="email" type="email">
```

### Implicit label

Wrap the control inside its label:

```html
<label>
  Email address
  <input name="email" type="email">
</label>
```

The explicit pattern is particularly convenient when a label and its control appear in separate parts of the markup.

- `for` matches the control's `id`, not its `name`.
- A placeholder is not a substitute for a label.
- Give each control a clear, persistent label that remains understandable after the user enters a value.

## 16. Placeholder

The `placeholder` attribute shows a short hint while a control is empty:

```html
<label for="email">Work email</label>
<input id="email" name="email" type="email" placeholder="name@example.com">
```

- Placeholder text disappears when the user types.
- It should supplement, not replace, a visible label.
- Placeholder styling can have low contrast; do not rely on it for essential instructions.
- Use help text near the control for instructions that users need while filling it in.

## 17. Required fields

The Boolean `required` attribute indicates that a value must be provided before normal browser submission:

```html
<label for="email">Email address (required)</label>
<input id="email" name="email" type="email" required>
```

- Browsers display their own validation feedback when a required value is missing.
- Communicate the requirement clearly to all users rather than relying only on browser error messages.
- For radio groups, requiring one member of the group can make one selection mandatory.
- Server-side checks remain necessary because client-side requirements can be bypassed.

## 18. Minimum, maximum, and step

Use the constraints appropriate to the input type:

```html
<input type="number" name="sampleCount" min="1" max="50" step="1">
<input type="date" name="studyDate" min="2025-01-01" max="2026-12-31">
<input type="text" name="code" minlength="4" maxlength="12">
```

- `min` and `max` set lower and upper bounds for applicable numeric or date controls.
- `step` defines valid increments for applicable numeric controls; its default is not always `1`.
- For text, use `minlength` and `maxlength` to constrain the number of characters.
- These attributes support browser validation; the application must still validate submitted data on the server.

## 19. Pattern validation

The `pattern` attribute specifies a regular expression that a non-empty text-like control must match:

```html
<label for="sample-code">Sample code</label>
<input
  id="sample-code"
  name="sampleCode"
  type="text"
  pattern="[A-Z]{2}-[0-9]{4}"
  title="Use two capital letters, a hyphen, and four digits, such as AB-1234">
<small id="sample-hint">Format: AB-1234</small>
```

- The browser checks that the **entire value** matches the pattern.
- A `pattern` does not make a field required; add `required` when an empty value is not permitted.
- Explain the expected format in visible text. The `title` can provide additional guidance but should not be the only instruction.
- Regular expressions can be easy to get wrong. Keep patterns understandable and do not use them to replace robust server-side validation.
- `pattern` applies to supported text-like controls; it is not the appropriate validation mechanism for every input type.

## 20. Grouping controls: `<fieldset>` and `<legend>`

`<fieldset>` groups related controls, and `<legend>` names the group:

```html
<fieldset>
  <legend>Contact preference</legend>
  <label><input type="radio" name="contact" value="email"> Email</label>
  <label><input type="radio" name="contact" value="phone"> Phone</label>
</fieldset>
```

- Group related checkboxes or radio buttons to communicate their relationship.
- The legend provides a group-level label; each control still needs its own label.
- A fieldset can be disabled as a whole with the Boolean `disabled` attribute.
- Do not add fieldsets merely for visual borders.

## 21. File uploads

Use `type="file"` to let users choose a local file:

```html
<form action="/upload" method="post" enctype="multipart/form-data">
  <label for="scan">Choose an image</label>
  <input
    id="scan"
    name="scan"
    type="file"
    accept="image/jpeg,image/png,image/webp"
    required>
  <button type="submit">Upload image</button>
</form>
```

- File uploads conventionally use `method="post"` and `enctype="multipart/form-data"`.
- `accept` is a chooser hint, **not** a security check. Validate the file type, size, and content on the server.
- `multiple` allows selecting more than one file.
- A browser normally submits the selected file when the form is submitted to a compatible endpoint.
- Browsers do not allow a page to silently read arbitrary local files; the user must select or provide the file.
- Tell users what files are accepted and surface useful errors.

## 22. Form validation

Form validation checks whether the submitted values meet the application's requirements.

### Native HTML constraint validation

HTML attributes can provide useful client-side checks:

```html
<form action="/register" method="post">
  <label for="email">Email address</label>
  <input id="email" name="email" type="email" required>

  <label for="age">Age</label>
  <input id="age" name="age" type="number" min="18" max="120" required>

  <button type="submit">Continue</button>
</form>
```

Common constraints include:

- `required`
- `min` and `max`
- `step`
- `minlength` and `maxlength`
- `pattern`
- Input-type checks such as `type="email"`

### `novalidate` and `formnovalidate`

- `novalidate` on `<form>` disables the browser's automatic constraint-validation UI when submitting.
- `formnovalidate` on a submit button skips that validation for that particular submit action.
- Use these only when the application intentionally provides its own equivalent validation and accessible feedback.

### Client-side and server-side validation

- **Client-side validation** provides quick feedback and improves the user experience, but users can bypass it.
- **Server-side validation** is essential: treat all client-provided data as untrusted, validate it on the server, and return meaningful errors.
- Client-side validation is not authorization, authentication, or protection against malicious input.
- Explain errors in text and associate them with the relevant field. Do not rely only on color.
- On validation failure, preserve valid user input where appropriate and help the user find and correct errors.

## Common form interview mistakes

- **A label's `for` matches the control's `id`; the control's `name` is used as the submitted-data key.**
- **An input without a `name` is normally not included in the submitted form data.**
- **A placeholder is not a label.**
- **Unchecked checkboxes and radio buttons are normally omitted from submitted data.**
- **`type="password"` masks text but does not encrypt it.**
- **`accept` on a file input is a hint, not upload validation.**
- **Client-side validation is not a substitute for server-side validation.**
- **An untyped button inside a form defaults to submit; set `type` explicitly.**
- **`required`, `min`, `max`, and `pattern` attributes can be bypassed; validate important data again on the server.**

## Quick comparison

| Requirement | HTML feature |
|---|---|
| Choose submission destination | `<form action="...">` |
| Retrieve/search data | `method="get"` |
| Submit data or request a state change | `method="post"` |
| Give a value a submission key | `name` |
| Create single-line control | `<input>` |
| Provide a persistent accessible name | `<label>` |
| Show a hint in an empty input | `placeholder` |
| Require a value | `required` |
| Limit values | `min`, `max`, `step`, `minlength`, `maxlength` |
| Constrain a text format | `pattern` |
| Group related controls | `<fieldset>` and `<legend>` |
| Select among choices | `<select>` and `<option>` |
| Enter multiple lines | `<textarea>` |
| Select a local file | `<input type="file">` |
| Submit form | `<button type="submit">` |
| Reset to initial values | `<button type="reset">` |

## Quick interview review

1. **What is the difference between `action` and `method`?**  
   `action` identifies the destination URL; `method` determines how the form sends its data.

2. **When should a form use GET or POST?**  
   GET is appropriate for retrieval, search, and bookmarkable parameters. POST is commonly used to submit data or change state.

3. **What is the difference between an input's `id` and `name`?**  
   `id` uniquely identifies an element in the document and connects it to a label; `name` identifies its key in submitted form data.

4. **How do checkboxes differ from radio buttons?**  
   Checkboxes permit independent selections; radio buttons with the same `name` form a group where one option can be selected.

5. **Is placeholder text an accessible replacement for a label?**  
   No. Placeholder text disappears as the user types and is not a reliable persistent name; use a `<label>`.

6. **Does `type="password"` secure a password?**  
   No. It masks the characters on screen. Secure transmission and server-side credential handling are separate requirements.

7. **Does `accept` guarantee a safe file upload?**  
   No. It influences the file chooser. The receiving application must validate uploads on the server.

8. **Why is client-side validation insufficient?**  
   A user can bypass or alter browser-side checks. The server must validate and authorize submitted data.

## Good practices to remember

- Give every control a clear label and a `name` when its value should be submitted.
- Choose an input type that matches the data and interaction.
- Group related controls with `<fieldset>` and `<legend>`.
- Use native validation for convenient feedback, and validate on the server as well.
- Explain required fields, expected formats, and errors in text.
- Use GET for retrieval and POST for submissions that change or create data.
- Use `multipart/form-data` for traditional file-upload form submissions.
- Make reset behavior deliberate and all actions clear.
