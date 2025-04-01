---
title: Tables
permalink: /markdown-for-github-pages/tables/
date: 2025-03-23
last_modified_date: 2025-03-31
order: 5
---

Tables display information in a clear and logical format. With tables, you can:

* Describe API inputs and outputs.
* Define technical terms.
* Show causes and effects.

Readers can easily scan tables for the information they need.

This page describes how to create tables.

## Basic table syntax

Use pipe's (`|`) and new lines to define the table columns and rows.

Pipes mark where columns start and end. Each table row has one pipe for each column plus one.

A row of dashes (`-`) in the second row makes the first row the header row.

For example, the following Markdown:

```text
| Column 1 | Column 2 |
|----------|----------|
| Column 1, Row 1 | Column 2, Row 1 |
| Column 1, Row 2 | Column 2, Row 2 |
```
renders to:

| Column 1 | Column 2 |
|----------|----------|
| Column 1, Row 1 | Column 2, Row 1 |
| Column 1, Row 2 | Column 2, Row 2 |

## Advanced table syntax

With Markdown's basic table syntax, you can use:

* Hyperlinks.
* Text decorations, like boldface, italic, and monospaced font.
* Images.

For more complicated structures, use the `<table>` HTML block. The `<table>` block lets you use:

* Subtables.
* Ordered and unordered lists.
* Multi-line code blocks

### Add a subtable to a table

To add a subtable, define a table in a table row.

```html
<table>
  <thead>
    <th>Column 1</th>
    <th>Column 2</th>
  </thead>
  <tbody>
    <tr>
      <td>Column 1, Row 1</td>
      <td>Column 2, Row 1</td>
    </tr>
    <tr>
      <td>Column 1, Row 2</td>
      <td><table>
        <thead>
          <th>Subcolumn 1</th>
          <th>Subcolumn 2</th>
        </thead>
        <tbody>
          <tr>
            <td>Subcolumn 1, Subrow 1</td>
            <td>Subcolumn 1, Subrow 2</td>
          </tr>
          <tr>
            <td>Subcolumn 1, Subrow 2</td>
            <td>Subcolumn 2, Subrow 2</td>
          </tr>
        </tbody>
      </table></td>
    </tr>
  </tbody>
</table>
```

renders to:

<table>
  <thead>
    <th>Column 1</th>
    <th>Column 2</th>
  </thead>
  <tbody>
    <tr>
      <td>Column 1, Row 1</td>
      <td>Column 2, Row 1</td>
    </tr>
    <tr>
      <td>Column 1, Row 2</td>
      <td><table>
        <thead>
          <th>Subcolumn 1</th>
          <th>Subcolumn 2</th>
        </thead>
        <tbody>
          <tr>
            <td>Subcolumn 1, Subrow 1</td>
            <td>Subcolumn 1, Subrow 2</td>
          </tr>
          <tr>
            <td>Subcolumn 1, Subrow 2</td>
            <td>Subcolumn 2, Subrow 2</td>
          </tr>
        </tbody>
      </table></td>
    </tr>
  </tbody>
</table>

### Add a list to a table

### Add a multi-line code block to a table
