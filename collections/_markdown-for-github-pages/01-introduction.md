---
title: Markdown for GitHub Pages
permalink: /markdown-for-github-pages/introduction/
date: 2025-03-21
last_modified_at: 2025-05-13
order: 1
---

In this tutorial, you'll learn how to contribute to a GitHub Pages project with some [basic Markdown formatting tools](/markdown-for-github-pages/basics/). These tools will help you create well-structured Markdown documents from scratch. You'll also learn how to add the [YAML front matter](/markdown-for-github-pages/frontmatter/) that Jekyll needs to render your documents.

## Introduction

Documentation is one of the most important parts of any software project.

A project's documentation tells the developers, stake holders, and end users:

* How the software works.
* Why you or your company created it.
* The reasons for choosing your technology over another.

Despite its importance, the documentation is often the last thing on a developer's mind. To get it done, many developers cobble together text snippets and screenshots into a word processor. That's if they create any documentation, at all.

It's hard to blame them. Clear writing is hard work. It isn't as glamorous as designing a code base. Nor is it as rewarding as seeing the system work. As a result, there is less incentive for a developer to spend time mastering their word processor over doing their other work.

You can't turn every developer into an expert writer, but there's a middle ground: a [_Docs as Code_][1] approach to technical documentation.

## The _Docs as Code_ approach

_Docs as Code_ uses many of the same concepts as a typical software development cycle:

* You write your documents in plain text, often in the same editor as you write your code.
* You save your documents in the same Version Control System (VCS) as the rest of your code base.
* You maintain the quality of your documentation with continuous integration and continuous development (CI/CD) pipelines.

By merging the writing process into their daily workflow, developers are better positioned to help create clearer, more complete documentation.

## _Docs as code_ and GitHub Pages

The final step in a _Docs as code_ approach is to render and display those plain text documents. One combination of options is [GitHub Pages and Jekyll][2].

The primary writing tool for GitHub Pages is Markdown. Markdown is a plain text format that uses "markup" to denote where to render:

* Headings
* Links
* Tables
* Images
* Other formatting options (for example, boldface, italics, or monospaced text)

GitHub Pages uses Jekyll to render plain text Markdown files into static HTML and CSS files. You can find plenty of examples of this kind of site in [GitHub's GitHub Pages example collection][3].

## How to use this tutorial

This tutorial is a reference guide to the most important Markdown features. Markdown is a feature-rich tool that can take a long time to master. Eventually, these features become second nature. In the meantime, though, a reference like this tutorial helps you get comfortable with the basics.

If you're brand new to Markdown, read this tutorial in order. If you have some Markdown experience, use the list of topics on the left side of the page to find a topic you want to learn more about.

With GitHub Pages, Jekyll, and some simple Markdown skills, you can create enticing, well-structured online documents. And, with a _Docs as Code_ approach, you can bring your development team along with you.

[1]: https://www.writethedocs.org/guide/docs-as-code/
[2]: https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/about-github-pages-and-jekyll
[3]: https://github.com/collections/github-pages-examples
