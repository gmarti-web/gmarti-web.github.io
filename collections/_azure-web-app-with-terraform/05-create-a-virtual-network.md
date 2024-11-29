---
title: Create a virtual network
permalink: /azure-web-app-with-terraform/create-a-virtual-network/
last_modified_at: 2024-11-27
order: 5
excerpt: Create a virtual network with Terraform.
---

A virtual network (Vnet) is software that acts like traditional networking
infrastructure, like switches and routers. We use virtual networks to control
how our application connects to the internet. We connect other resources to our
virtual network by breaking the network into sections, called subnets. We
define rules for how internet traffic can interact with our resources. Azure
calls these rules network security groups.

This page describes how to create:

- A virtual network
- A subnet
- A network security group with one network security group rule

## Define the virtual network

1. Open the `main.tf` file.
1. Add the following Terraform code to the bottom of the file:

    ```hcl
    resource "azurerm_virtual_network" "vnet" {
      # Reference the resource group we defined earlier
      resource_group_name = azurerm_resource_group.rg.name
      location            = azurerm_resource_group.rg.location
      name                = "azure-web-app-vnet"
      address_space       = ["10.0.0.0/16"]
    }
    ```

     | Configuration   | Description                                                                                                                                                                                                                                           | Example              |
     |-----------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------|
     | `name`          | The name of your VNet.                                                                                                                                                                                                                                | `azure-web-app-vent` |
     | `address_space` | The amount of memory you want to dedicate to your virutal network. It determines how many, and what kinds, of IP addresses your network can use. [Read more about address spaces](https://www.techtarget.com/searchstorage/definition/address-space). | `10.0.0.0/16`        |

    See the [Terraform Registry](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/virtual_network#argument-reference) to learn more about the `azurerm_virtual_network` resource's available arguments.

1. Save your changes to the `main.tf` file.

## Create a subnet

A subnet is a digital slice of the virtual network. We use subnets to connect
the virtual network to the Internet and other Azure resources.

1. In the `main.tf` file, add the following Terraform code:

    ```hcl
    resource "azurerm_subnet" "subnet" {
        resource_group_name  = azurerm_resource_group.rg.name
        virtual_network_name = azurerm_virtual_network.vnet.name
        name                 = "defaultsubnet"
        address_prefixes     = ["10.0.2.0/24"]
        service_endpoints    = ["Microsoft.Sql"] # This lets our web app's SQL server connect to the network.
    }
    ```

     | Configuration       | Description                                                                                                                                                                                  | Example         |
     |---------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------|
     | `name`              | The name of your subnet.                                                                                                                                                                     | `defaultsubnet` |
     | `address_prefixes`  | The subset of your virtual network's address space reserved for this subnet.                                                                                                                 | `10.0.2.0/24`   |
     | `service_endpoints` | Standard aliases for Azure resources. [Read more about the available service endpoints](https://learn.microsoft.com/en-us/azure/virtual-network/virtual-network-service-endpoints-overview). | `Microsoft.Sql` |

    See the [Terraform
    Registry](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/subnet#argument-reference)
    to learn more about the `azurerm_subnet` resource's available arguments.

1. Save your changes to the `main.tf` file

## Create a network security group

A network security group is a set of rules that define how traffic moves in and
out of the virtual network.

1. In the `main.tf` file, add the following Terraform code:

    ```hcl
    resource "azurerm_network_security_group" "nsg" {
        resource_group_name = azurerm_resource_group.rg.name
        location            = azurerm_resource_group.rg.location
        name                = "azure-web-app-nsg"
    }

    # We attach the security group to a subnet of the virtual network.
    resource "azurerm_subnet_network_security_group_association" "nsg_assoc" {
        subnet_id                 = azurerm_subnet.subnet.id
        network_security_group_id = azurerm_network_security_group.nsg.id
    }
    ```

     | Configuration | Description                             | Example              |
     |---------------|-----------------------------------------|----------------------|
     | `name`        | The name of the network security group. | `azure-webn-app-nsg` |

    See the [Terraform
    Registry](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/network_security_group#argument-reference)
    to learn more about the `azurerm_network_security_group` resource's
    available arguments.

1. Save the `main.tf` file.

## Create a network security group rule

A network security group rule is a single rule in a network security group.

For this tutorial, we create one security rule group to allow incoming traffic
on port `22`. This lets us SSH into a virtual machine within the network.

1. In the `main.tf` file, add the following Terraform code:

    ```hcl
    resource "azurerm_network_security_rule" "nsg_22" {
        resource_group_name         = azurerm_resource_group.rg.name
        network_security_group_name = azurerm_network_security_group.nsg.name
        name                        = "azure-web-app-ssh-nsg-rule"
        priority                    = 300
        access                      = "Allow"
        direction                   = "Inbound"

        # We allow TCP traffic to port 22 so we can SSH into the network.
        protocol                    = "Tcp"
        source_port_range           = "*"
        destination_port_range      = "22"
        source_address_prefix       = "*"
        destination_address_prefix  = "*"
    }
    ```

    | Configuration | Description | Example |
    |---------------|-------------|---------|
    | `name` | The name of the network security group rule. | `azure-web-app-ssh-nsg-rule` |
    | `network_security_group_name` | The name of the network security group that owns this rule. | `azure-web-app-nsg` |
    | `priority` | The priority given to the rule in a list of rules. Network security groups evaluate rules with lower priority numbers first. | `300` |
    | `access` | This rule's action in response to the defined traffic, either `Allow` or `Deny`. | `Allow` |
    | `direction` | The direction to allow traffic, either `Inbound` or `Outbound`. | `Inbound` |
    | `protocol` | The name of the traffic protocol. | `Tcp` |
    | traffic sources (`source_port_range` and `source_address_prefix`) | Individual ports or IP address of the traffic sender. | `*` (All ports or all IP addresses) |
    | traffic destinations (`destination_port_range` and `destination_address_prefix`) | Individual ports or IP address of the traffic receiver. | `22` (Allow computers to SSH into the VNet) |

    See the [Terraform
    Registry](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/network_security_rule#argument-reference)
    to learn more about the `azurerm_network_security_rule` resource's
    available arguments.

1. Save your changes to the `main.tf` file.

## Learn more

- [Azure Vnet concepts and best practices](https://learn.microsoft.com/en-us/azure/virtual-network/concepts-and-best-practices)
- [Network security groups overview](https://learn.microsoft.com/en-us/azure/virtual-network/network-security-groups-overview)
- [How network security groups filter network traffic](https://learn.microsoft.com/en-us/azure/virtual-network/network-security-group-how-it-works)

