---
title: Knowledge base with GitHub Pages audience analysis
date: 2024-12-14
last_modified_at: 2024-12-26
categories:
    - GitHub Pages
    - Knowledge bases
excerpt: An audience anlaysis for my knowledge base with GitHub Pages tutorial.
---

## Writer-centered analysis

| Gatekeepers |
|-------------|
| N/A |

<table>
    <thead>
        <tr>
            <th>&nbsp;</th>
            <th>Audience</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <th>Tertiary</th>
            <td><ul>
                <li>General public</li>
                <li>Writers evaluating knowledge base options</li>
            </ul></td>
        </tr>
        <tr>
            <th>Secondary</th>
            <td><ul>
                <li>Technical content managers</li>
                <li>Developer team managers</li>
                <li>Writers and developers familiar wth GitHub, Markdown, or Jekyll</li>
            </ul></td>
        </tr>
        <tr>
            <th>Primary</th>
            <td>Writers and developers with no experience with Markdown or Jekyll</td>
        </tr>
        <tr>
            <th>Writer</th>
            <td>Greg Martinez</td>
        </tr>
    </tbody>
</table>

## Reader analysis

<table>
    <thead>
        <tr>
            <th>&nbsp;</th>
            <th>Needs</th>
            <th>Values</th>
            <th>Attitudes</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <th>Primary</th>
            <td><ul>
                <li>Clear examples, in code and graphics</li>
                <li>Reason for using GitHub and Markdown</li>
                <li>Cheat sheet that informs but doesn't overwhelm</li>
                <li>Quickest path to create a document</li>
            </ul></td>
            <td><ul>
                <li>Clarty</li>
                <li>Sequential steps</li>
                <li>Scannability</li>
            </ul></td>
            <td><ul>
                <li>Busy</li>
                <li>Skeptical</li>
                <li>Task-oriented</li>
            </ul></td>
        </tr>
        <tr>
            <th>Secondary</th>
            <td><ul>
                <li>Implementation examples</li>
                <li>Knowledge base featuers</li>
                <li>Comparison to other knowledge bases</li>
                <li>version control features</li>
            </ul></td>
            <td><ul>
                <li>Clarity</li>
                <li>Objectivity</li>
                <li>Low buy-in costs</li>
            </ul></td>
            <td><ul>
                <li>Busy</li>
                <li>Ambivalent to specific technology</li>
            </ul></td>
        </tr>
        <tr>
            <th>Tertiary</th>
            <td><ul>
                <li>Explanation for why they would use this technology</li>
                <li>Examples of real-world knowledge base strateges</li>
                <li>Comparison to other potential knowledge base strategies</li>
            </ul></td>
            <td><ul>
                <li>Clarity</li>
                <li>Thoroughness</li>
                <li>Objectivity</li>
            </ul></td>
            <td><ul>
                <li>Curious</li>
                <li>Skeptical</li>
            </ul></td>
        </tr>
    </tbody>
</table>

## Reader context analysis

| | Physical context | Mobile context | Economic context | Ethical context |
|-|------------------|----------------|------------------|----------------|
| **Primary Readers** | Posts on the internet. | Post on the internet scaled to the size of the reader's device. | Creating documentation with minimal effort. | How to make sure the documentation is accurate and easy for others to read? |
| **Reader's organization** | Posts on the internet. | Posts on the internet scaled to the size of the reader's device. | Minimal time and resources spent adopting the technology. | Are developers able to incorporate the effort to adopt this technology into their normal, busy workload? |
| **Reader's industry** | Posts on the internet. | Posts on the internet scaled to the size of the reader's device. | Cost of training developers and writers to work in a CI/CD documentation pipeline. | Can the technology create a knowledge base that is accessible by everyone? |

## Audience's desired outcome

The primary audience's desired outcome is to add documentation with minimal
effort to a shared knowledge base. To keep this tutorial focused on simple
Markdown articles, it doesn't cover [Liquid](https://shopify.github.io/liquid/)
template language or [jekyll site
structure](https://jekyllrb.com/docs/structure/) features. It does, however,
explain how to set up a GitHub Pages service with jekyll. It also covers
[jekyll front matter](https://jekyllrb.com/docs/front-matter/) so that jekyll
can rendor the learner's articles.

## Outline of deliverable

```md
# Knowledge base with GitHub

## Introduction

### Install `ruby` and `bundler`

#### Install `ruby` for windows

#### Install `ruby` for macOS

#### Install `ruby` for linux

#### Install `bundler`

### Create a `Gemfile`

## Create a GitHub repository

### Set up workflow to deploy your knowledge base

#### Deploy with GitHub Pages

#### Deploy with bring-your-own (BYO) app service

## Create a Markdown page

### Create a blank Markdown file

### Add frontmatter

#### Basic frontmatter

#### Child page frontmatter

### Add content

#### Markdown basics

##### Headings

##### Lists

###### Ordered lists

###### Unordered lists

##### Tables

##### Links

##### Images

## Preview your changes locally

## Push to your GitHub repository

## Summary

## FAQs
```
