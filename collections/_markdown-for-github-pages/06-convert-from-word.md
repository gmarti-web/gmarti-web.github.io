---
title: Convert Word documents to Markdown
permalink: /markdown-for-github-pages/convert-from-word/
date: 2025-03-23
last_modified_at: 2025-04-08
order: 7
---

## The `pandoc` tool

The [`pandoc`](https://pandoc.org/index.html) can convert documents from one format to another.

## Word document to Markdown

To convert you Word document to Markdown:

1. Install [`pandoc`](https://pandoc.org/installing.html).

  Confirm the installation by running the following command:

  ```console
  pandoc --verison
  ```

1. Run the following command:

  ```console
  pandoc \
    --extract-media ./images \
    -o path/to/markdown/file.md \
    path/to/word/file.docx
  ```

Pandoc saves your converted document to `path/to/markdown/file.md`. It saves any images from your Word document to a folder called `images`.

