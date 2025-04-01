---
title: Basics
permalink: /markdown-for-github-pages/basics/
date: 2025-03-23
last_modified_date: 2025-03-31
order: 3
---

Basic Markdown syntax adds simple formatting to a document. The basics include:

* Headings and subheadings.
* Text formatting, like boldface, italics, and monospaced.
* Hyperlinks.

This page describes how to add each of these basic Markdown syntax elements.

## Headings

Use hashes (`#`) to create headings and subheadings.

| Heading level | Markdown syntax | Example |
|---------------|-----------------|---------|
| Level 1 | `#` | `# Level 1 heading` |
| Level 2 | `##` | `## Level 2 heading` |
| Level 3 | `###` | `### Level 3 heading` |
| Level 4 | `####` | `#### Level 4 heading` |
| Level 5 | `#####` | `##### Level 5 heading` |
| Level 6 | `######` | `###### Level 6 heading` |

The following image shows what these headings render to in the browser:

{% include figure
  popup=true
  image_path="/assets/images/portfolio/markdown-for-github-pages/heading-example.png"
  alt="A screenshot of the six Markdown heading levels"
  caption="Figure 1: Six Markdown heading levels."
%}

## Text formats

Markdown lets you format your text with plain text decorators.

### Use boldface font

Surround a word or phrase with two asterisks (`**`) to make it boldface.

For example, the following Markdown text:

```text
This phrase uses **boldface** font.
```

renders to:

This phrase uses **boldface** font.

### Use italic font

Surround a word or phrase with an underscore (`_`) to make it italic.

For example, the following Markdown text:

```text
This phrase uses _italics_.
```

renders to:

This phrase uses _italics_.

### Use monospaced font

Surround a word with backticks (\`) to make it monospaced. Use monospaced font for code snippets and code blocks.

For example, the following Markdown text:

```text
This phrase uses `monospaced` font.
```

renders to:

This phrase uses `monospaced` font.

To make multi-line code blocks, surround a text block with three backticks (\`\`\`). For the code block to use syntax highlights, add the code language to the end of the first backtick triplet.

For example, the following Markdown text:

``````text
```python
import pandas

df = pandas.from_csv("mydata.csv")
```
``````

renders to:

```python
import pandas

df = pandas.from_csv("mydata.csv")
```

## Hyperlinks

Add hyperlinks to your document with brackets (`[]`) and parentheses (`()`).

### Link to external sites

Hyperlinks can link any other site on the internet.

For example, the following Markdown text:

```text
[This sentence links to https://google.com](https://google.com).
```

renders to:

[This sentence links to https://google.com](https://google.com).

### Link to other pages in your site

Use the [`link` Liquid tag](https://jekyllrb.com/docs/liquid/tags/#links) to link to another page in your site.

For example, the following Markdown:

```text
[This sentence links to my About page]({% raw %}{% link _pages/about.md %}{% endraw %}).
```

renders to:

[This sentence links to my About page]({% link _pages/about.md %}).

### Link to specific sections on the same page

Add a hyperlink to any section of the current page with the heading name.

For example, the following Markdown:

```text
[This sentence links to this page's **Headings** section](#headings).
```

renders to:

[This sentence links to this page's **Headings** section](#headings).
