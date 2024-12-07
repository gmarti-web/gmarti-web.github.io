---
title: Project plan
last_modified_at: 2024-10-16
categories:
    - PTW310
excerpt: The project plan for my PTW310 portfolio project.
---

## Subject

My portfolio project is a blog-style tutorial on using the Azure Terraform registry
to create a simple web application. For this project, a simple web application
includes a networking setup, a server, and a MYSQL database. The project will have:

- An easy-to-use navigation menu. This lets my readers find the sections they need
to do their work.
- Background and instructions for each section. This gives my readers
more context about the problem they’re solving. Busy readers can skip directly to
the information they need using hyperlinks.
- Resources for readers to learn more about each topic. This lets readers dig deeper
into the topics that interest them.
- An end-to-end example of using multiple services in a single script to create
a web application. This gives readers a reference for using the tutorial to solve
a real problem.

The tutorial must:

- Use tools consistently for examples and code snippets. This makes the tutorial
easy to follow. These tools are:
  - Visual Studio Code as my integrated development environment (IDE).
  - Terraform as my configuration language.
  - Azure as my cloud environment.
- Follow the “Every Page is Page One” model. This model lets readers start learning
from any page they land on. If a section builds on earlier concepts, I’ll give readers
the links to those concepts at the top of the section.
- Use tested, runnable code. This ensures the tutorial’s information is correct.
A reader must be able to copy-and-paste code from the tutorial into their terminal
or code editor and run it.

The tutorial will cover how to create Azure resources only. It won’t cover:

- How the reader can add style to the web application with CSS.
- How the reader can add interactive pieces to the web application with JavaScript.
- How the reader can register a custom domain for the web application.

## Purpose

I chose this tutorial for my portfolio project because I want to write a long-form
technical article. This article will be about a subject that I am skilled in, specifically
Azure and Terraform. I’m comfortable enough with these technologies to write and
assess a tutorial on using them. Adding this tutorial to my portfolio will show
that I can write clearly and effectively about software development in the cloud.

This tutorial will help cloud engineers work programmatically in their cloud environment.
This can be difficult for engineers who don’t have experience with common developer
tools. Most engineers can search the internet to find what they need. Others need
instructions related to their own environment. They need documentation with concrete
examples that they can apply at once.

## Audience

This tutorial’s audience is junior cloud engineers. These engineers have experience
with basic concepts in the cloud (AWS, Azure, or GCP). They know how to download
applications, run commands in their computer’s terminal, and navigate their cloud
environment’s web interface. They don’t, however, have the technical knowledge to
write scripts from scratch. They’d follow this tutorial to complete a task on behalf
of a client.

The needs, values, and attitudes of this audience are:

<table>
    <tr>
        <th>Needs</th>
        <td><ul>
            <li>Specific examples</li>
            <li>Clear and readable code</li>
            <li>Visual aides</li>
            <li>Troubleshooting recommendations</li>
        </ul></td>
    </tr>
    <tr>
        <th>Values</th>
        <td><ul>
            <li>Client satisfaction</li>
            <li>Flexibility</li>
            <li>Repeatable outcomes</li>
        </ul></td>
    </tr>
    <tr>
        <th>Attitudes</th>
        <td><ul>
            <li>Busy</li>
            <li>Task-oriented</li>
        </ul></td>
    </tr>
</table>

## Format and tools

I’ll write this tutorial with Markdown and HTML. I’ll use Jekyll for to convert
them to static web pages. I’ll host these on an Azure static web app.

