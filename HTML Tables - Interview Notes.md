# HTML Tables — Interview Preparation

## 1. When to use a table

Use an HTML table to present **tabular data**: information organized into rows and columns where the relationships between values matter.

Examples include a comparison of model metrics, a schedule, or a dataset summary.

Do not use a table just to arrange page layout. Use CSS Grid, Flexbox, or another layout method for page design.

## 2. Table structure

A basic table uses `<table>` to contain rows. Rows contain header cells (`<th>`) or data cells (`<td>`):

```html
<table>
  <tr>
    <th scope="col">Stage</th>
    <th scope="col">Status</th>
  </tr>
  <tr>
    <td>Image preparation</td>
    <td>Available</td>
  </tr>
</table>
```

`<table>` gives the data a tabular structure. Browsers do not add table headings automatically; include the appropriate header cells yourself.

## 3. Table rows: `<tr>`

`<tr>` represents a **table row**. A row is made up of table header cells, data cells, or—where appropriate—other valid table-structure elements.

```html
<tr>
  <td>Green-channel preview</td>
  <td>Ready</td>
</tr>
```

Rows create the horizontal groups of data in a table.

## 4. Table headings: `<th>`

`<th>` represents a **header cell**, identifying a column or row. Use `scope` to clarify the direction of a header when appropriate:

```html
<th scope="col">Model</th>
<th scope="row">CNN</th>
```

- `scope="col"` identifies a header for a column.
- `scope="row"` identifies a header for a row.
- `scope="colgroup"` and `scope="rowgroup"` can identify group headers in more complex tables.
- Browsers usually style `<th>` in bold and centered by default, but its important role is semantic association, not appearance.

Do not use `<td>` and CSS bolding as substitutes for a real header cell.

## 5. Table data: `<td>`

`<td>` represents a regular data cell:

```html
<td>92.4%</td>
```

A data cell belongs to a table row and usually has meaning in relation to one or more row or column headers. Write concise values and avoid merging cells when a simpler structure is easier to understand.

## 6. Table captions: `<caption>`

`<caption>` gives the table a concise, descriptive title:

```html
<table>
  <caption>Preprocessing stage availability</caption>
  <tr>
    <th scope="col">Stage</th>
    <th scope="col">Availability</th>
  </tr>
  <tr>
    <td>Green-channel preview</td>
    <td>Available</td>
  </tr>
</table>
```

- A `<caption>` should be the first child of its `<table>`.
- It helps users identify the table's subject, including users who navigate between tables with assistive technology.
- For a longer description, provide additional text outside the caption and associate it as appropriate.

## 7. Table head, body, and footer

The table can be divided into:

- `<thead>`: header rows describing columns or groups.
- `<tbody>`: the main data rows.
- `<tfoot>`: summary or footer rows, such as a total.

```html
<table>
  <caption>Example image preparation durations</caption>
  <thead>
    <tr>
      <th scope="col">Operation</th>
      <th scope="col">Duration</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th scope="row">Channel extraction</th>
      <td>Not measured</td>
    </tr>
    <tr>
      <th scope="row">Contrast preview</th>
      <td>Not measured</td>
    </tr>
  </tbody>
  <tfoot>
    <tr>
      <th scope="row">Result</th>
      <td>No performance results provided</td>
    </tr>
  </tfoot>
</table>
```

- `<thead>`, `<tbody>`, and `<tfoot>` help group related rows and make the markup easier to understand.
- A table can contain one `<thead>` and one `<tfoot>`, and may have one or more `<tbody>` groups.
- The browser can create an implicit `<tbody>` when rows are written directly inside `<table>`; explicit grouping makes the structure clearer.
- `<tfoot>` is for actual summary or footer data—not simply to style the last row.
- These elements do not add accessibility to a table by themselves; meaningful `<th>` cells and associations still matter.

## 8. `rowspan`

`rowspan` makes a cell span multiple rows:

```html
<table>
  <tr>
    <th scope="rowgroup" rowspan="2">Preprocessing</th>
    <th scope="row">Green channel</th>
    <td>Available</td>
  </tr>
  <tr>
    <th scope="row">Contrast preview</th>
    <td>Available</td>
  </tr>
</table>
```

- The value indicates the number of rows the cell spans.
- Cells occupied by that span must not be repeated in the following rows.
- Complex spans can make header relationships harder to follow; keep merged cells limited and the table understandable.

## 9. `colspan`

`colspan` makes a cell span multiple columns:

```html
<table>
  <tr>
    <th scope="col" colspan="2">Image preparation</th>
  </tr>
  <tr>
    <th scope="col">Operation</th>
    <th scope="col">Status</th>
  </tr>
  <tr>
    <td>Green-channel preview</td>
    <td>Available</td>
  </tr>
</table>
```

- The value indicates how many columns the cell spans.
- The other rows must still form a coherent table grid.
- For a group heading that applies to several columns, consider whether `<colgroup>` and correct header associations are needed.

## 10. Accessible table relationships

For a simple table, use `<th scope="col">` and, where useful, `<th scope="row">`:

```html
<table>
  <caption>Project processing steps</caption>
  <thead>
    <tr>
      <th scope="col">Step</th>
      <th scope="col">Browser preview</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th scope="row">Green channel</th>
      <td>Available</td>
    </tr>
  </tbody>
</table>
```

For more complex tables where headers cannot be clearly determined by row and column scope alone, give header cells unique `id` values and associate data cells with `headers`:

```html
<table>
  <tr>
    <th id="group" colspan="2">Image previews</th>
  </tr>
  <tr>
    <th id="preview-type" scope="col">Preview</th>
    <th id="availability" scope="col">Availability</th>
  </tr>
  <tr>
    <th id="green-row" scope="row">Green channel</th>
    <td headers="group availability green-row">Available</td>
  </tr>
</table>
```

Use `headers` and `id` only when needed: simpler tables with correct `<th>` and `scope` are easier to maintain and navigate.

## 11. Responsive tables

Wide tables can overflow on narrow screens. Keep the table readable and provide horizontal scrolling when necessary:

```html
<div class="table-scroll" role="region" aria-label="Model comparison" tabindex="0">
  <table>
    <!-- Table content -->
  </table>
</div>
```

```css
.table-scroll {
  max-width: 100%;
  overflow-x: auto;
}

table {
  width: 100%;
  border-collapse: collapse;
}
```

Use a focusable, named scroll region when keyboard users need a way to scroll the table container. Avoid breaking the association between header and data cells when adapting the visual layout for mobile.

## Quick comparison

| Element or attribute | Purpose |
|---|---|
| `<table>` | Contains tabular data |
| `<tr>` | Table row |
| `<th>` | Header cell |
| `<td>` | Data cell |
| `<caption>` | Describes the table's subject |
| `<thead>` | Groups header rows |
| `<tbody>` | Groups main data rows |
| `<tfoot>` | Groups summary/footer rows |
| `scope` | Identifies the row or column a header applies to |
| `rowspan` | Makes a cell span multiple rows |
| `colspan` | Makes a cell span multiple columns |

## Quick interview review

1. **When should you use an HTML table?**  
   When presenting tabular data with meaningful row and column relationships—not for page layout.

2. **How do `<th>` and `<td>` differ?**  
   `<th>` marks a header cell; `<td>` holds regular data.

3. **What does `scope` do?**  
   It identifies whether a header applies to a row, column, row group, or column group.

4. **What are `<thead>`, `<tbody>`, and `<tfoot>` for?**  
   They group a table's header, body, and footer rows, respectively.

5. **How do `rowspan` and `colspan` differ?**  
   `rowspan` spans rows vertically; `colspan` spans columns horizontally.

6. **Why add a `<caption>`?**  
   It provides a descriptive title that helps users, including assistive-technology users, identify the table.

7. **How can a wide table work on a small screen?**  
   Put it in an appropriately labelled, keyboard-accessible container with `overflow-x: auto` when horizontal scrolling is needed.

## Good practices to remember

- Use tables for data, not for layout.
- Give each table a useful caption where it improves understanding.
- Use `<th>` for actual headers and identify their scope.
- Prefer a simple row-and-column structure; merged cells complicate navigation.
- Use `<thead>`, `<tbody>`, and `<tfoot>` to group rows by purpose.
- Test large tables with a keyboard and a narrow viewport.
