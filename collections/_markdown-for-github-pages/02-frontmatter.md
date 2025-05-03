---
title: Front matter
permalink: /markdown-for-github-pages/frontmatter/
date: 2025-03-21
last_modified_at: 2025-05-03
order: 2
---

Front matter tells Jekyll how to render Markdown pages on your site. It defines the page's title, layout, address, and other metadata. If a page doesn't have this information, Jekyll won't render it.

This page describes:

* How to write basic front matter.
* Some common metadata elements used in front matter.
* Where to find other resources to learn more advanced front matter use cases.

## Basic front matter structure

Front matter goes at the top of each Markdown page. Three dashes (`---`) separate the front matter from the rest of the document.

For example, a Markdown document with front matter might look like this:

```text
<!-- START OF PAGE -->

---
title: My page title
---

<!-- MAIN CONTENT -->
```

## Common front matter elements

You can add any metadata you want to a page's front matter. Some common, helpful metadata elements include:

| YAML element | Description |
|----------|-------------|
| `title` | The page title. |
| `permalink` | The page's address. The permalink element lets you link to this page from other pages in your site. |
| `parent` | The page's "parent." "Children" pages are subpages of their parent page. |
| `last_modified_date` | The page's last modified date. This lets readers know when you last updated a page. |

For example, the front matter section of a page in your site's "Tutorials" section might look like this:

```text
---
title: Tutorial example 1
permalink: /tutorials/example1/
parent: Tutorials
last_modified_date: 2025-03-24
---

<!-- MAIN CONTENT -->
```

## Advanced front matter uses

You can reference metadata defined in one page's front matter from any other page in your site. This expands your site's capabilities to:

* Create template HTML files to include on different pages.
* Define data once and use it many times.
* Generate page content dynamically.

See [Jekyll's front matter documentation](https://jekyllrb.com/docs/front-matter/) to learn more.

See [the Liquid template language reference](https://shopify.github.io/liquid/) to learn how to add logic to your documentation using metadata.

To learn more about your Jekyll theme's specific front matter options, see your theme's documentation.

