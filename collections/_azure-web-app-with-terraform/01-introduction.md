---
title: Introduction
permalink: /azure-web-app-with-terraform/introduction/
last_modified_at: 2024-11-20
order: 1
excerpt: Learn how to use Terraform to create the basic web app components in Azure.
---

<!-- TODO: Define a web app (Disambiguation!) -->

A simple web app has three components:

<div>
  <dl>
      <dt>Virtual network</dt>
      <dd>Software that replaces traditional networking infrastructure, like routers and switches</dd>
      <dt>Virtual machine</dt>
      <dd>A digital environment that behaves like a physical computer.</dd>
      <dt>Database</dt>
      <dd>A storage system that saves data.</dd>
  </dl>
</div>

Together, these components give you a connected machine that is always on, connected to the internet, and available for others to see. This means you can save applications, services, or static web pages here and access them anywhere, anytime. With the reliability of the cloud, you don't have to worry about the host's physical environment. Compare this with hosting your content on your home computer, where you must manage its power, cooling, and continuous operation. A web app in Azure lets you focus on improving your content rather than maintaining physical hardware.

## Purpose and scope

This tutorial describes how to use Terraform to create the basic components for a simple web app. It includes:

- Downloading, installing, and configuring the Azure CLI
- Setting up a Terraform workspace
- Writing Terraform configuration files
- Planning, applying, and destroying Terraform resources

If you work in the cloud or are interested in learning industry-standard concepts, this tutorial will help you get started with code-first infrastructure strategies.
