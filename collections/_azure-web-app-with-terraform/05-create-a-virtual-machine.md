---
title: Create a Virtual Machine
permalink: /azure-web-app-with-terraform/create-a-virtual-machine/
date: 2024-11-09
last_modified_at: 2024-11-11
order: 5
excerpt: Create a virtual machine with Terraform.
---

## Background

TBD

## Create a virtual machine

1. Open the `main.tf` file.
1. Add the following Terraform code to the bottom of the file:

    ```hcl
    resource "azurerm_network_interface" "nic" {
        name                = "azure-web-app-nic"
        location            = "westus2"
        resource_group_name = azurerm_resource_group.rg.name
        ip_configuration {
            name                          = "internal"
            private_ip_address_allocation = "Dynamic"
        }
    }
    resource "azurerm_linux_virtual_machine" "vm" {
        name                  = "azure-web-app-vm"
        resource_group_name   = azurerm_resource_group.rg.name
        location              = azurerm_resource_group.rg.location
        size                  = "Standard_F2"
        admin_username        = "adminuser"
        admin_password        = "myp@sswoRD11!"
        network_interface_ids = [azurerm_network_interface.nic.id]
        os_disk {
            caching              = "ReadWrite"
            storage_account_type = "Standard_LRS"
        }
        source_image_reference {
            publisher = "canonical"
            offer     = "0001-com-ubuntu-server-jammy"
            sku       = "22_04-lts-gen2"
            version   = "latest"
        }
    }
    ```

## Troubleshooting

TBD

## Learn more

TBD
