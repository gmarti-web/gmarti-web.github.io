---
title: Front matter
permalink: /markdown-for-github-pages/frontmatter/
last_modified_date: 2025-03-26
order: 2
---

Front matter tells Jekyll how to render Markdown pages on your site. It defines the page's title, layout, URL, and other metadata. If a page doesn't have this information, Jekyll won't render it.

This page describes:

* How to wrte basic front matter.
* Some common metadata elements used in front matter.
* Where to find other resources to learn more advanced front matter use cases.

## Basic front matter structure

Front matter goes at the top of each Markdown page. It's marked off from the rest of the document with three dashes (`---`).

For example, here's the start of a Markdown document with front matter:

```md
<!-- START OF PAGE -->

---
title: My page title
---

<!-- MAIN CONTENT -->
```

## Common front matter elements

You can add any metadata you want to a page's front matter. There are, however, some common, helpful metadata to consider.

| YAML element | Description |
|----------|-------------|
| `title` | The page title. |
| `permalink` | The page URL. The permalink element lets you link to this page from other pages in your site. |
| `parent` | The page's "parent." "Children" pages are organized as subpages of their parent page. |
| `last_modified_date` | The page's last modified date. This lets readers know when a page was last updated. |

For example, here's the front matter element of a page that is a subpage of the "Tutorials" section:

```yaml
---
title: Tutorial example 1
permalink: /tutorials/example1/
parent: Tutorials
last_modified_date: 2025-03-24
---

# MAIN CONTENT
```

## Advanced front matter uses

You can reference metadata defined in one page's front matter from any other page in your site.

See [Jekyll's front matter documentation](https://jekyllrb.com/docs/front-matter/) to learn more.

See [the Liquid template language reference](https://shopify.github.io/liquid/) to learn how to add logic to your documentation using metadata.

To learn more about your Jekyll theme's specific front matter options, see your theme's documentation.

