---
title: FAQs
permalink: /azure-web-app-with-terraform/faqs/
last_modified_at: 2024-11-29
order: 10
excerpt: Explore frequently asked questions to learn more about Azure and Terraform.
---

## Terraform

### What is Terraform?

Terraform is an infrastructure-as-code tool that lets you define resources in
human-readable configuration files.

[Learn more about Terraform](https://developer.hashicorp.com/terraform/intro).

{% include learn-terraform.html %}

### What is the Terraform Registry?

The Terraform Registry is a public collection of resource packages that you can
use to create your infrastructure. The Registry has code maintained by
third-party developers, including the three major cloud providers (AWS, Azure,
and GCP).

[Explore the Terraform Registry](https://registry.terraform.io/?product_intent=terraform).

### What is the `azurerm` provider?

The `azurerm` provider is a code package that Microsoft maintains and hosts in
the Terraform Registry. This provider lets you create different resources in
Azure.

[See the `azurerm`
documentation](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs)
to learn more about how to create different resources.


### How does Terraform keep track of my environment's configuration?

Terraform uses your environment's state to keep track of its real-world
configuration. It keeps this state in a file named `terraform.tfstate`.

[Learn more about how Terraform manages your environment's
state](https://developer.hashicorp.com/terraform/language/state).

## Web apps and Azure

### What is a web app?

{{ site.data.azure-web-app-with-terraform.definitions.web-app }}

### What is an Azure resource group?

{{ site.data.azure-web-app-with-terraform.definitions.resource-group }}

### What is a virtual network?

{{ site.data.azure-web-app-with-terraform.definitions.virtual-network }}

### What is a virtual machine?

{{ site.data.azure-web-app-with-terraform.definitions.virtual-machine }}

### Why do I need a network security group?

A network security group keeps your network safe from threats over the public
internet. [Learn more about network security
groups](https://learn.microsoft.com/en-us/azure/virtual-network/network-security-groups-overview).

### Why do I need to add a network security rule to allow inbound traffic on port 22?

You must allow inbound traffic on port 22 before you can connect to a virtual
machine (VM) in your network. [Learn more about how to connect to a
VM](https://learn.microsoft.com/en-us/azure/virtual-machines/linux-vm-connect?tabs=Linux).

