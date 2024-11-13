---
title: Introduction
permalink: /azure-web-app-with-terraform/introduction/
date: 2024-11-03
last_modified_at: 2024-11-13
order: 1
excerpt: Learn how to use Terraform to create the basic web app components in Azure.
---

## Background

A simple web app has three components:

<div>
<dl>
    <dt>Virtual network</dt>
    <dd>Software that simulates traditional networking infrastructure, like routers and switches</dd>
    <dt>Virtual machine</dt>
    <dd>A portion of computing resources based in a server farm.</dd>
    <dt>Database</dt>
    <dd>A SQL- or NoSQL-based storage system that saves data.</dd>
</dl>
</div>

Together, these components give you a connected machine that is always on, connected to the internet, and available for others to see.

## Purpose and scope

This tutorial describes how to use Terraform to create the basic components for a simple web app. It includes:

- Downloading, installing, and configuring the Azure CLI
- Setting up a Terraform workspace
- Writing Terraform configuration files
- Planning, applying, and destroying Terraform resources

If you work in the cloud or are interested in learning industry-standard concepts, like infrastructure-as-code, this tutorial will help you get started with code-first infrastructure strategies.
