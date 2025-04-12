---
title: Introduction
permalink: /markdown-for-github-pages/introduction/
date: 2025-03-21
last_modified_at: 2025-04-12
order: 1
---

In any software project, one of the most important parts is the documentation. A project's documentation tells the developers, stake holders, and end users:

* How the software works.
* Why you created it.
* Your reasons for choosing one technology over another.

Despite its importance, the documentation is often the last thing on a developer's mind. To get it done, they just cobble together text snippets and screenshots into a word processor. That's if they create any documentation, at all.

It's hard to blame them. Clear writing isn't as glamorous as designing a code base. Nor is it as rewarding as seeing the system work. As a result, there is less incentive for a developer to spend time mastering their word processor over their other work.

While we can't turn every developer into an expert writer, we can reach a middle ground. That middle ground is a Docs-as-Code approach to technical documentation.

## The Docs-as-Code approach

A Docs-as-Code approach uses many of the same concepts as a typical software development cycle:

* You write your documents in plain text, often in the same editor as you write your code.
* You save your documents in the same version control system (VCS) as the rest of your code base.
* You maintain the quality and standards for your documentation with continuous integration and continuous development (CI/CD) pipelines.

By merging the writing process into their daily workflow, developers are better positioned to create clearer, more complete documentation.

## Docs-as-Code and GitHub Pages

The final step in a Docs-as-Code approach is to render and display those plain text documents. One combination among many options is GitHub Pages and Jekyll.

GitHub Pages renders plain text Markdown files into static HTML and CSS files with a rendering tool called Jekyll. Jekyll combines your documentation and added metadata into an online documentation site. You can find plenty of examples of this kind of site:

* Site 1
* Site 2
* Site 3

The primary tool you use in a Docs-as-Code approach with GitHub Pages and Jekyll is Markdown. Markdown is a plain text format that uses "markup" to denote where to render:

* Headings
* Links
* Tables
* Images
* Other formatting options (for example, boldface, italics, or monospaced text)

In this tutorial, you'll learn some [basic Markdown formatting tools](/markdown-for-github-pages/basics/). These tools will help you create well-structured Markdown documents from scratch, including the required [YAML front matter](/markdown-for-github-pages/frontmatter/). You'll also learn how to [quickly convert existing documentation](/markdown-for-github-pages/convert-from-word/), likely written in Microsoft Word documents, into Markdown with the `pandoc` tool.

