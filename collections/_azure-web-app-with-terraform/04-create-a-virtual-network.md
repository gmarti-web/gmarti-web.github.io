---
title: Create a virtual network
permalink: /azure-web-app-with-terraform/create-a-virtual-network/
date: 2024-11-09
last_modified_at: 2024-11-13
order: 4
excerpt: Create a virtual network with Terraform.
---

## Background

TBD

## Create a VNet

1. Open the `main.tf` file.
1. Add the following Terraform code to the bottom of the file:

    ```hcl
    resource "azurerm_virtual_network" "vnet" {
        name                = "azure-web-app-vnet"
        location            = "westus2"
        resource_group_name = azurerm_resource_group.rg.name
        address_space       = ["10.0.0.0/16"]
    }
    ```

1. Save the `main.tf` file.

## Troubleshooting

TBD

## Learn more

TBD
