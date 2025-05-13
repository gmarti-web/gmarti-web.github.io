---
title: Convert Word documents to Markdown
permalink: /markdown-for-github-pages/convert-from-word/
date: 2025-03-23
last_modified_at: 2025-05-12
order: 7
---

Many developers write their documentation with a program like Microsoft Word. Word is widely available and easy to use. All you need to do is start writing. In a demanding field like software development, the simplest tool is often the best one.

Word, though, has its drawbacks:

* Contextual elements, like code blocks or collapsible sections, are hard or impossible to add.
* Word's bells and whistles distract from writing.
* Documents hard to version control.

GitHub pages solves these issues. That doesn't mean, though, you have to rewrite your Word document in Markdown. Instead, you can use a tool like `pandoc` to convert them for you.

## The `pandoc` tool

The [`pandoc`](https://pandoc.org/index.html) can convert documents from one format to another.

To convert your Word document to Markdown:

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

## Review the output

It's important to check that the conversion was successful. There may be artifacts or ill-formatted tables that you must clean up before submitting the document to your version control system.

You also must add the required [YAML front matter](/markdown-for-github-pages/frontmatter/). Without the front matter, Jekyll won't render your document.

