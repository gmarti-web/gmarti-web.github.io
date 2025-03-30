---
title: Basics
permalink: /markdown-for-github-pages/basics/
last_modified_date: 2025-03-26
order: 3
---

Markdown basics help add simple formatting to a document. The basics include:

* Headings and subheadings.
* Text formatting, like boldface, italics, and monospaced.
* Hyperlinks.

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

The following image shows what these headings look like in the browser:

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

```console
This phrase uses **boldface** font.
```

renders to:

This phrase uses **boldface** font.

### Use italic font

Surround a word or phrase with an underscore (`_`) to make it italic.

For example, the following Markdown text:

```console
This phrase uses _italics_.
```

renders to:

This phrase uses _italics_.

### Use monospaced font

Surround a word with backticks (\`) to make it monospaced.

For example, the following Markdown text:

```console
This phrase uses `monospaced` font.
```

renders to:

This phrase uses `monospaced` font.

Use monospaced font for code snippets and code blocks. To make multi-line code blocks, surround a text block with three backticks (\`\`\`). For the code block to use syntax highlights, add the code language to the end of the first backtick triplet.

For example, the following Markdown text:

````console
```python
import pandas

df = pandas.from_csv("mydata.csv")
```
````

renders to:

```python
import pandas

df = pandas.from_csv("mydata.csv")
```

