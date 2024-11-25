---
title: Create a Virtual Machine
permalink: /azure-web-app-with-terraform/create-a-virtual-machine/
last_modified_at: 2024-11-15
order: 6
excerpt: Create a virtual machine with Terraform.
---

A virtual machine is a digital environment that behaves like a physical computer. Azure Virtual machines can run Windows or Linux operating systems. You can use virtual machines to manage access to other services, to run resource-heavy calculations, or to host content. For this tutorial, we want a virtual machine that users can access over the internet.

To make our virutal machine accessible to users, it needs a steady online address. To create this address, we create a network interface with a static public IP address. With a public IP address, we can define network security rules that allow other computers to access our virtual machine.

This page describes how to create:

- A static public IP address
- A network interface
- A Linux virtual machine

## Define your virtual machine's components

To create a virtual machine, define the following:

### Public IP

A static public IP gives your virtual machine a consistent online address. If we don't create a static IP, our computer's address may change at any time.

| Configuration | Definition | Example |
|---------------|------------|---------|
| `name` | The name of your IP address. | `azure-web-app-ip` |
| `allocation_method` | The way Azure assigns the IP address, either `Static` or `Dynamic`. | `Static` |

### Network interface

A network interface connects a virtual machine to a virutal network.

| Configuration | Definition | Example |
|---------------|------------|---------|
| `name` | The name of your network interface. | `azure-web-app-nic` |
| `ip_configuration` | The IP connection between the virtual network and your public IP address. | `ip_configuration {`<br/>`name="public"`<br/>`subnet_id=azurerm_subnet.subnet.id`<br/>`private_ip_address_allocation="Dynamic"`<br/>`public_ip_address_id=azurerm_public_ip.ip4.id`<br/>`}` |

### Virtual machine

This is the virtual machine definition.

| Configuration | Definition | Example |
|---------------|------------|---------|
| `name` | The name of the virtual machine. | `azure-web-app-vm` |
| `size` | The size of the virtual machine. | `Standard_F2` |
| `admin_username` | The admin user's username. | `adminuser` |
| `admin_password` | The admin user's password. | `myp@sswoRD11!` |
| `disable_password_authentication` | Disallow users to access the machine with a password. | `false` |
| `network_interface_ids` | The network interfaces that connect the machine to the virtual network. | `azurerm_network_interface.nic.id` |
| `os_disk` | The machine's storage disk. | `os_disk {`<br/>`caching="ReadWrite"`<br/>`storage_account_type="Standard_LRS"`<br/>`}` |
| `source_image_reference` | The machine's operating system. | `source_image_reference {`<br/>`publisher="canonical"`<br/>`offer="0001-com-ubuntu-server-jammy`<br/>`sku="22_04-lts"`<br/>`version="latest"`<br/>`}` |


## Create a virtual machine

1. Open the `main.tf` file.
1. Add the following Terraform code to the bottom of the file:

    ```hcl
    resource "azurerm_public_ip" "ip4" {
        resource_group_name = azurerm_resource_group.rg.name
        location            = azurerm_resource_group.rg.location
        allocation_method   = "Static"
        name                = "azure-web-app-ip"

        lifecycle {
            create_before_destroy = true
        }
    }

    resource "azurerm_network_interface" "nic" {
        location            = azurerm_resource_group.rg.location
        resource_group_name = azurerm_resource_group.rg.name
        name                = "azure-web-app-nic"
        ip_configuration {
            name                          = "public"
            subnet_id                     = azurerm_subnet.subnet.id
            private_ip_address_allocation = "Dynamic"
            public_ip_address_id          = azurerm_public_ip.ip4.id
        }
    }

    resource "azurerm_linux_virtual_machine" "vm" {
        resource_group_name             = azurerm_resource_group.rg.name
        location                        = azurerm_resource_group.rg.location
        name                            = "azure-web-app-vm"
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

## Learn more

- [Terraform: `azurerm_public_ip`](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/public_ip)
- [Terraform: `azurerm_network_interface`](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/network_interface)
- [Terraform: `azurerm_linux_virtual_machine`](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/linux_virtual_machine)
- [Azure virtual machine series](https://azure.microsoft.com/en-us/pricing/details/virtual-machines/series/?msockid=329aaa3c4d516c1904efbe154c7c6df5)

