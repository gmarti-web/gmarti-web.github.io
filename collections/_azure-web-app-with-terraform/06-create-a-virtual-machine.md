---
title: Create a Virtual Machine
permalink: /azure-web-app-with-terraform/create-a-virtual-machine/
last_modified_at: 2024-11-15
order: 6
excerpt: Create a virtual machine with Terraform.
---

A virtual machine is a digital environment that behaves like a physical computer. Azure Virtual machines can run Windows or Linux operating systems. You can use virtual machines to manage access to other services, to run resource-heavy calculations, or to host content. For this tutorial, we want a virtual machine that users can access over the internet.

To make our virutal machine accessible to users, it needs a steady address online. To create this address, we create a network interface with a static public IP address. With a public IP address, we can define network security rules that allow other computers to access our virtual machine.

This page describes how to create:

- A static public IP address
- A network interface
- A Linux virtual machine

## Create a virtual machine

1. Open the `main.tf` file.
1. Add the following Terraform code to the bottom of the file:

    ```hcl
    resource "azurerm_public_ip" "ip4" {
        name                = "azure-web-app-ip"
        resource_group_name = azurerm_resource_group.rg.name
        location            = azurerm_resource_group.rg.location
        allocation_method   = "Static"

        lifecycle {
            create_before_destroy = true
        }
    }

    resource "azurerm_network_interface" "nic" {
        name                = "azure-web-app-nic"
        location            = azurerm_resource_group.rg.location
        resource_group_name = azurerm_resource_group.rg.name
        ip_configuration {
            name                          = "public"
            subnet_id                     = azurerm_subnet.subnet.id
            private_ip_address_allocation = "Dynamic"
            public_ip_address_id          = azurerm_public_ip.ip4.id
        }
    }

    resource "azurerm_linux_virtual_machine" "vm" {
        name                            = "azure-web-app-vm"
        resource_group_name             = azurerm_resource_group.rg.name
        location                        = azurerm_resource_group.rg.location
        size                            = "Standard_F2"
        admin_username                  = "adminuser"
        admin_password                  = "myp@sswoRD11!"
        disable_password_authentication = false
        network_interface_ids           = [azurerm_network_interface.nic.id]
        os_disk {
            caching              = "ReadWrite"
            storage_account_type = "Standard_LRS"
        }
        source_image_reference {
            publisher = "canonical"
            offer     = "0001-com-ubuntu-server-jammy"
            sku       = "22_04-lts"
            version   = "latest"
        }
    }
    ```

### Define a network interface

TBD

### Define an OS disk

TBD

### Define the source image reference

TBD

## Troubleshooting

TBD

## Learn more

TBD

