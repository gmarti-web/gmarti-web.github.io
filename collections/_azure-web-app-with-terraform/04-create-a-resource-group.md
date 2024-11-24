---
title: Create a resource group
permalink: /azure-web-app-with-terraform/create-a-resource-group/
last_updated_at: 2024-11-24
order: 4
excerpt: Create an Azure resource group with Terraform.
---

An Azure resource group is a logical group of related resources. All Azure resources must belong to a resource group.

This page describes how to create a resource group with Terraform.

## Create a resource group

1. Create a new file and enter the following Terraform code:

    ```hcl
    resource "azurerm_resource_group" "rg" {
        name     = "azure-web-app-with-terraform-rg"
        location = "westus2"
    }
    ```

1. Save this file as `main.tf`.

    We'll create the rest of the infrastructure for this tutorial in this file.

We'll reference this resource group when we create the remaining Azure resources.

## Learn more

- [Manage Azure resource groups by using the Azure portal](https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/manage-resource-groups-portal)
- [Terraform: `azurerm_resource_group`](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/resource_group)

