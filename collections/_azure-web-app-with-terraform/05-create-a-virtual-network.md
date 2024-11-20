---
title: Create a virtual network
permalink: /azure-web-app-with-terraform/create-a-virtual-network/
last_modified_at: 2024-11-15
order: 5
excerpt: Create a virtual network with Terraform.
---

A virtual network is a digital representation of traditional networking infrastructure, like switches and routers. We use virtual networks to control how our application connects to the internet. We connect other resources to our virtual network by breaking the network into sections, called subnets.

This page describes how to create:

- A virtual network
- A subnet
- A network security group with one network security group rule

## Create a VNet

1. Open the `main.tf` file.
1. Add the following Terraform code to the bottom of the file:

    ```hcl
    resource "azurerm_virtual_network" "vnet" {
        name                = "azure-web-app-vnet"
        location            = azurerm_resource_group.rg.location
        resource_group_name = azurerm_resource_group.rg.name
        address_space       = ["10.0.0.0/16"]
    }

    resource "azurerm_subnet" "subnet" {
        name                 = "internalsubnet"
        resource_group_name  = azurerm_resource_group.rg.name
        virtual_network_name = azurerm_virtual_network.vnet.name
        address_prefixes     = ["10.0.2.0/24"]
        service_endpoints    = ["Microsoft.Sql"]
    }

    resource "azurerm_network_security_group" "nsg" {
        name                = "azure-web-app-nsg"
        resource_group_name = azurerm_resource_group.rg.name
        location            = azurerm_resource_group.rg.location
    }

    resource "azurerm_network_security_rule" "nsg_22" {
        name                        = "azure-web-app-ssh-nsg-rule"
        resource_group_name         = azurerm_resource_group.rg.name
        priority                    = 300
        access                      = "Allow"
        direction                   = "Inbound"
        protocol                    = "Tcp"
        source_port_range           = "*"
        destination_port_range      = "22"
        source_address_prefix       = "*"
        destination_address_prefix  = "*"
        network_security_group_name = azurerm_network_security_group.nsg.name
    }

    resource "azurerm_subnet_network_security_group_association" "nsg_assoc" {
        subnet_id                 = azurerm_subnet.subnet.id
        network_security_group_id = azurerm_network_security_group.nsg.id
    }
    ```

1. Save the `main.tf` file.

### Define an address space

TBD

### Define a subnet

TBD


## Troubleshooting

TBD

## Learn more

TBD
