---
title: Tables
permalink: /markdown-for-github-pages/tables/
date: 2025-03-23
last_modified_date: 2025-04-05
order: 5
---

Tables display information in a clear and logical format. They let readers easily scan your document for the information they need.

With tables, you can:

* Describe API inputs and outputs.
* Define technical terms.
* Show causes and effects.

This page describes how to create tables.

## Basic table syntax

Use pipes (`|`) and new lines to define a table's columns and rows.

Pipes mark where columns start and end. Each table row has one pipe plus one for each column.

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

### Add a hyperlink to a table

You can add a hyperlink to any cell in a table.

[Learn how to add hyperlinks](/markdown-for-github-pages/basics/#hyperlinks).

For example, the following Markdown:

```text
| Column 1 | Column 2 |
|----------|----------|
| [This sentence links to google.com](https://google.com) | Column 2, Row 1 |
| Column 1, Row 2 | Column 2, Row 2 |
```

renders to:

| Column 1 | Column 2 |
|----------|----------|
| [This sentence links to google.com](https://google.com) | Column 2, Row 1 |
| Column 1, Row 2 | Column 2, Row 2 |

### Format texts in a table

You can format any text in a table.

[Learn how to format text](/markdown-for-github-pages/basics/#text-formats).

For example, the following Markdown:

```text
| Column 1 | Column 2 |
|----------|----------|
| **Column 1**, Row 1 | Column 2, Row 1 |
| Column 1, Row 2 | _Column 2_, Row 2 |
| `Column 1, Row 3` | Column 2, Row 3 |
```

renders to:

| Column 1 | Column 2 |
|----------|----------|
| **Column 1**, Row 1 | Column 2, Row 1 |
| Column 1, Row 2 | _Column 2_, Row 2 |
| `Column 1, Row 3` | Column 2, Row 3 |

### Add images to a table

You can add an image to any cell in a table

[Learn how to add images](/markdown-for-github-pages/images/).

For example, the following Markdown:

```text
| Column 1 | Column 2 |
|----------|----------|
| Column 1, Row 1 | Column 2, Row 1 |
| Column 1, Row 2 | Column 2, Row 2 |
| Column 1, Row 3 | ![small icon](/assets/favicon/favicon-96x96.png "Small icon image") |
```

renders to:

| Column 1 | Column 2 |
|----------|----------|
| Column 1, Row 1 | Column 2, Row 1 |
| Column 1, Row 2 | Column 2, Row 2 |
| Column 1, Row 3 | ![small icon](/assets/favicon/favicon-96x96.png "Small icon image") |

## Advanced table syntax

Use the `<table>` HTML block to add more complicated elements, like:

* Subtables.
* Ordered and unordered lists.
* Multi-line code blocks

### Understand the `<table>` HTML block

The `<table>` HTML block has two subsections:

<dl>
  <dt><code>&lt;thead&gt;</code></dt>
  <dd>The table head section.<ul><li>Define each column name in this section with <code>&lt;th&gt;</code> elements.</li></ul></dd>
  <dt><code>&lt;tbody&gt;</code></dt>
  <dd>The table body section.<ul>
    <li>Define each table row with a <code>&lt;tr&gt;</code> (table row) section.</li>
    <li>Define each column value in a row with <code>&lt;td&gt;</code> (table data) section.</li>
  </ul></dd>
</dl>

### Add a list to a table

To add a list to a table, define an ordered or unordered list in a table row.

For example, the following HTML:

```html
<table>
  <thead>
    <th>Column 1</th>
    <th>Column 2</th>
  </thead>
  <tbody>
    <tr>
      <td>Column 1, Row 1</td>
      <td>Column 2, Row 2</td>
    </tr>
    <tr>
      <td>Column 1, Row 2</td>
      <td><ul>
        <li>Item 1</li>
        <li>Item 2</li>
      </ul></td>
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
      <td><ul>
        <li>Item 1</li>
        <li>Item 2</li>
      </ul></td>
    </tr>
  </tbody>
</table>

### Add a multi-line code block to a table

To add a multi-line code block, define preformatted code block.

For example, the following HTML:

```html
<table>
  <thead>
    <th>Column 1</th>
    <th>Column 2</th>
  </thead>
  <tbody>
    <tr>
      <td>Column 1, Row 1</td>
      <td><code><pre>
import pandas as pd

df = pd.read_csv("file.csv")
      </pre></code></td>
    </tr>
    <tr>
      <td>Column 1, Row 2</td>
      <td>Column 2, Row 2</td>
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
      <td><code><pre>
import pandas as pd

df = pd.read_csv("file.csv")
      </pre></code></td>
    </tr>
    <tr>
      <td>Column 1, Row 2</td>
      <td>Column 2, Row 2</td>
    </tr>
  </tbody>
</table>

### Add a subtable to a table

To add a subtable, define a table in a table row.

For example, the following HTML:

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
            <td>Subcolumn 2, Subrow 1</td>
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
            <td>Subcolumn 2, Subrow 1</td>
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
