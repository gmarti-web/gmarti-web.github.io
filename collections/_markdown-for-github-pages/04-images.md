---
title: Images
permalink: /markdown-for-github-pages/images/
date: 2025-03-23
last_modified_date: 2025-04-05
order: 4
---

Images add concise explanations of complex topics to your technical documentation . They break up the text and give the reader another medium through which they can understand the content.

This page describes how to add images in two ways.

## Basic syntax

Add images to a document with simple Markdown syntax.

```markdown
![alt-text](path/to/img.jpg "image title")
```

* `alt-text`: The image's alternative text. Alternative text improves the reading experience when using a screen reader.
* `path/to/img.jpg`: The relative path to the image file.
* `"image title"`: The image's title.

For example, the following Markdown:

```text
![An example image](/assets/favicon/favicon-96x96.png "This is the image's title")
```

renders to:

![An example image](/assets/favicon/favicon-96x96.png "This is the image's title")

## Advanced syntax

To add a caption or custom style to an image, use the `figure` HTML block.

For example, the following HTML:

```html
<figure>
  <img src="/assets/favicon/favicon-96x96.png" alt="An example image" title="This is the image's title" style="width:25%;height:25%">
  <figcaption>This is the image's caption</figcaption>
</figure>
```

renders to:

<figure>
  <img src="/assets/favicon/favicon-96x96.png" alt="An example image" title="This is the image's title" style="width:25%;height:25%">
  <figcaption>This is the image's caption</figcaption>
</figure>

