---
title: How to create an Azure web app with Terraform
permalink: /portfolio/how-to-create-an-azure-web-app-with-terraform/
last_modified_at: 2024-11-29
excerpt: Learn how to use Terraform to create the basic web app components in Azure.
---

## Introduction

{{ site.data.azure-web-app-with-terraform.definitions.web-app }}

Web apps vary in complexity. The examples above have many features, like
personal accounts, payment processors, and external integrations with other web
apps. The core of a web app, however, comprises three components:

<div>
  <dl>
      <dt>Virtual network</dt>
      <dd>Software that replaces traditional networking infrastructure, like routers and switches.</dd>
      <dt>Virtual machine</dt>
      <dd>A digital environment that behaves like a physical computer.</dd>
      <dt>Database</dt>
      <dd>A storage system that saves data.</dd>
  </dl>
</div>

Together, these components give you a connected machine that is always on,
connected to the internet, and available for others to visit. This means you
can save applications, services, or static web pages here and access them
anywhere, anytime. With the reliability of the cloud, you don't have to worry
about the host's physical environment. Compare this with hosting your content
on your home computer where you must manage its power, cooling, and continuous
operation. A web app in Azure lets you focus on improving your content rather
than maintaining physical hardware.

This tutorial describes how to use Terraform to create the basic components for
a simple web app. It includes:

- Downloading, installing, and configuring the Azure CLI
- Setting up a Terraform workspace
- Writing Terraform configuration files
- Planning, applying, and destroying Terraform resources

If you work in the cloud or are interested in learning industry-standard
concepts, this tutorial will help you get started with infrastructure-as-code
strategies.

## Prerequisites

Before you can follow this tutorial, you must:

- Create an Azure account
- Install the Azure command-line interface (CLI)
- Install the Terraform command-line interface (CLI)

Optionally, you can save your work in a [GitHub repository](https://github.com/).

### Create a free Azure account

{% include create-azure-account.html %}

### Set up the Azure CLI

{% include login-to-azure-cli.html download=true %}

### Install the Terraform CLI

1. Go to [Install Terraform](https://developer.hashicorp.com/terraform/install).
1. Download the Terraform package for your operating system:

    - [Windows](https://developer.hashicorp.com/terraform/install#windows)
    - [macOS](https://developer.hashicorp.com/terraform/install#darwin)
    - [Linux or Windows Subsystem for Linux (WSL)](https://developer.hashicorp.com/terraform/install#linux)

1. To confirm the installation, run the following command:

    ```console
    terraform -version
    ```

    The command returns the version of the downloaded Terraform package.

    {%
      include figure
      popup=true
      image_path="/assets/images/terraform-download-finish.png"
      alt="terraform-download-finish"
      caption="Terraform version command"
    %}

{% include learn-terraform.html %}

## Connect to Azure with Terraform

We'll authenticate to the Terraform `azurerm` provider with
the Azure CLI.

{%- capture tip-content -%} The [azurerm
documentation](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs#authenticating-to-azure)
in the Terraform Registry lists different ways to authenticate to Azure. If you
want to automate this process, authenticate with a service principal or managed
service identity instead. {% endcapture %}

{% include tip-notice.html content=tip-content %}

### Log into the Azure CLI

{% include login-to-azure-cli.html %}

### Create a `providers.tf` file

1. Create a folder called `azure-web-app-with-terraform`.

    ```console
    mkdir azure-web-app-with-terraform
    ```

1. Change directories into that folder.

    ```console
    cd azure-web-app-with-terraform
    ```

    {%- capture tip_content -%}
    To get your Azure subscription ID, run the following command in your terminal:
    <br/><br/>
    `az account show`
    <br/><br/>
    This returns a JSON response in your terminal. Your subscription ID is in the `id` field.
    {% endcapture %}

    {% include tip-notice.html content=tip_content %}

1. Create a new file and enter the following Terraform code:

    ```hcl
    terraform {
        required_providers {
            azurerm = {
            source = "hashicorp/azurerm"
            version = "=4.9.0"
            }
        }
    }

    provider "azurerm" {
        features {}
        subscription_id = "<YOUR-AZURE-SUBSCRIPTION-ID>"
    }
    ```

1. Save this file as `providers.tf`.

    This file defines your Terraform providers. You can define any number of
    providers in your Terraform project. For this tutorial, we'll use only the
    `azurerm` provider.

### Initialize your Terraform workspace

In your terminal, run the following command:

```console
terraform init
```

This command installs the providers and creates a `.terraform.lock.hcl` file.
This file records which providers the workspace uses so Terraform installs the
same versions when you run `terraform init` in the future.

{% include figure
  popup=true
  image_path="/assets/images/terraform-init.png"
  alt="terraform-init"
  caption="Terraform initialize confirmation message"
%}

You're now ready to create Azure resources with Terraform.

## Create the resource group

An Azure resource group is a logical group of related resources. All Azure
resources must belong to a resource group.

To define the resource group:

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

## Create a virtual network

A virtual network (Vnet) is software that acts like traditional networking
infrastructure, like switches and routers. We use virtual networks to control
how our application connects to the internet. We connect other resources to our
virtual network by breaking the network into sections, called subnets. We
define rules for how internet traffic can interact with our resources. Azure
calls these rules network security groups.

### Define the virtual network

To define the virtual network:

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

### Define a subnet

A subnet is a digital slice of the virtual network. We use subnets to connect
the virtual network to the Internet and other Azure resources.

To define a subnet:

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

### Define a network security group

A network security group is a set of rules that define how traffic moves in and
out of the virtual network.

To define a network security group:

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

### Define a network security group rule

A network security group rule is a single rule in a network security group.

For this tutorial, we create one security rule group to allow incoming traffic
on port `22`. This lets us SSH into a virtual machine within the network.

To define a network security group rule:

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


## Create a virtual machine

A virtual machine (VM) is a digital environment that acts like a physical
computer. Azure Virtual machines can run Windows or Linux operating systems.
You can use virtual machines to manage access to other services, to run
resource-heavy calculations, or to host content. For this tutorial, we want a
virtual machine that serves content that users can access over the internet.

To make our virutal machine accessible, we must give it a reliable online
address. To do so, we create a network interface with a static public IP
address. With a public IP address, we can define network security rules that
allow other computers to access our virtual machine.

### Define a static IP address

A static public IP gives your virtual machine a consistent online address. If
we don't create a static IP, our virtual machine's address may change at any
time.

To define a static IP address:

1. Open the `main.tf` file.
1. Add the following Terraform code to the bottom of the file:

    ```hcl
    resource "azurerm_public_ip" "ip4" {
        resource_group_name = azurerm_resource_group.rg.name
        location            = azurerm_resource_group.rg.location
        name                = "azure-web-app-ip"
        allocation_method   = "Static"

        lifecycle {
            create_before_destroy = true
        }
    }
    ```

    | Configuration | Definition | Example |
    |---------------|------------|---------|
    | `name` | The name of your IP address. | `azure-web-app-ip` |
    | `allocation_method` | The way Azure assigns the IP address, either `Static` or `Dynamic`. | `Static` |

1. Save your changes to the `main.tf` file.

### Define a network interface

A network interface creates a connection between a virtual machine in a virtual
network and the public internet.

To define a network interface:

1. In the `main.tf` file, add the following Terraform code:

    ```hcl
    resource "azurerm_network_interface" "nic" {
        resource_group_name = azurerm_resource_group.rg.name
        location            = azurerm_resource_group.rg.location
        name                = "azure-web-app-nic"
        ip_configuration {
            name                          = "public"
            subnet_id                     = azurerm_subnet.subnet.id
            private_ip_address_allocation = "Dynamic"
            public_ip_address_id          = azurerm_public_ip.ip4.id
        }
    }
    ```

    | Configuration | Definition | Example |
    |---------------|------------|---------|
    | `name` | The name of your network interface. | `azure-web-app-nic` |
    | `ip_configuration` | The IP connection between the virtual network and your public IP address. | `ip_configuration {`<br/>`name="public"`<br/>`subnet_id=azurerm_subnet.subnet.id`<br/>`private_ip_address_allocation="Dynamic"`<br/>`public_ip_address_id=azurerm_public_ip.ip4.id`<br/>`}` |

    See the [Terraform
    Registry](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/network_interface#argument-reference)
    to learn more about the `azurerm_network_interface` resource's available
    arguments.

### Define the virtual machine

To define the virtual machine:

1. In the `main.tf` file, add the following Terraform code:

    ```hcl
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

    | Configuration | Definition | Example |
    |---------------|------------|---------|
    | `name` | The name of the virtual machine. | `azure-web-app-vm` |
    | `size` | The size of the virtual machine. | `Standard_F2` |
    | `admin_username` | The admin user's username. | `adminuser` |
    | `admin_password` | The admin user's password. | `myp@sswoRD11!` |
    | `disable_password`<br/>`_authentication` | Disallow users to access the machine with a password. | `false` |
    | `network_interface`<br/>`_ids` | The network interfaces that connect the machine to the virtual network. | `azurerm_network_interface`<br/>`.nic.id` |
    | `os_disk` | The machine's storage disk. | `os_disk {`<br/>`caching="ReadWrite"`<br/>`storage_account_type="Standard_LRS"`<br/>`}` |
    | `source_image`<br/>`_reference` | The machine's operating system. | `source_image_reference {`<br/>`publisher="canonical"`<br/>`offer="0001-com-ubuntu-server-jammy`<br/>`sku="22_04-lts"`<br/>`version="latest"`<br/>`}` |

    See the [Terraform
    Registry](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/linux_virtual_machine#argument-reference)
    to learn more about the `azurerm_linux_virtual_machine` resource's
    available arguments.

## Create an Azure SQL server

An Azure SQL server is a relational database management system (RDBMS). It
saves data in tables that can be filtered and sliced with SQL queries. Our web
app needs a SQL server to save and retrieve data from users.

We must allow the SQL server to connect to the virtual network we created
earlier. We do that with a virtual network rule.

To define the Azure SQL server:

1. Open the `main.tf` file.
1. Add the following Terraform code to the bottom of the file:

    ```hcl
    resource "azurerm_mssql_server" "mssql_server" {
        resource_group_name          = azurerm_resource_group.rg.name
        location                     = azurerm_resource_group.rg.location
        name                         = "azure-web-app-mssqlserver"
        version                      = "12.0"
        administrator_login          = "Example-Administrator"
        administrator_login_password = "myp@sswoRD11!"
        minimum_tls_version          = "1.2"
    }

    resource "azurerm_mssql_virtual_network_rule" "vnetrule" {
        name      = "sql-vnet-rule"
        server_id = azurerm_mssql_server.mssql_server.id
        subnet_id = azurerm_subnet.subnet.id
    }
    ```

    | Configuration | Definition | Example |
    |---------------|------------|---------|
    | `name` | The name of your SQL server. | `azure-web-app-mssqlserver` |
    | `version` | The SQL server version. | `12.0` |
    | `administrator_login` | The administrator's login username. | `Exmaple-Administrator` |
    | `administrator_login_password` | The administrator's login password. | `myp@sswoRD11!` |
    | `minimum_tls_version` | The minimum TLS version the server allows. | `1.2` |

    See the [Terraform
    Registry](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/mssql_server#argument-reference)
    to learn more about the `azurerm_mssql_server` resource's available
    arguments. 

1. Save the `main.tf` file.


## Deploy your resource

Terraform uses the definitions in the `maint.tf` file to create resources in
Azure. It determines in what order resources need to be created. And, it tracks
your resources for you, so you can change them in the `main.tf` file at any
time without starting from scratch.

1. In your terminal, run the following command:

    ```console
    terraform plan
    ```

    This command tells you how Terraform will build your infrastructure. It
    tallys up how many resources your Terraform code will add, change, or
    destroy.

    {% include figure
      popup=true
      image_path="/assets/images/terraform-plan.png"
      alt="terraform-plan"
      caption="`terraform plan` output"
    %}

    {% include
      tip-notice.html
      content="Always review the plan before you create or edit resources. This is your chance
      to catch any misconfigurations that might harm or accidentally delete your resources."
    %}

1. After you review the plan, run the following command:

    ```console
    terraform apply
    ```

    The command asks you to confirm. To do so, enter `yes`.

    {% include figure
      popup=true
      image_path="/assets/images/terraform-apply-confirm.png"
      alt="terraform-apply-confirm"
      caption="`terraform apply` confirmation message"
    %}

    This creates your infrastructure. This may take a few minutes.

The results are displayed in your terminal.

{% include figure
  popup=true
  image_path="/assets/images/terraform-apply-complete.png"
  alt="terraform-apply-complete"
  caption="`terraform apply` completion message"
%}

Your resources are ready to use in Azure. See your new resource group in the
[Azure portal](https://portal.azure.com).

{% include figure
  popup=true
  image_path="/assets/images/azure-resources.png"
  alt="azure-resources"
  caption="Azure resource group details"
%}


## Wrap-up

In this tutorial, we:

- Created an Azure resource group to organize our web app components.
- Created an Azure virtual network that lets us connect our resources to the internet.
- Created an Azure virtual machine with a public IP address and a network interface.
- Created an Azure SQL server and connected it to our virtual network.

You now have the basic infrastructure for a simple web app! And, because the
infrastructure is defined as code, you can recreate this exact set of resources
in any environment with the same configuration script.

### Delete resources

Delete, or destroy, the resources we created in this tutorial to avoid any
unexpected Azure charges.

1. In your terminal, run the following command:

    ```console
    terraform destroy
    ```

    This command tells you which resources Terraform will destroy.

1. Enter `yes` to confirm that you want to destroy these resources.

    {% include figure
      popup=true
      image_path="/assets/images/terraform-destroy-confirm.png"
      alt="terraform-destroy-confirm"
      caption="`terraform destroy` confirmation message"
    %}

A message appears when Terraform successfully destroys your resources.

{% include figure
  popup=true
  image_path="/assets/images/terraform-destroy-complete.png"
  alt="terraform-destroy-complete"
  caption="`terraform apply` completion message"
%}

### Explore other projects

- [Learn about Terraform modules](https://developer.hashicorp.com/terraform/language/modules)
- [15+ Terraform real-time project examples](https://www.projectpro.io/article/terraform-projects-examples/621)


## FAQs

<details>
  <summary><strong>Terraform</strong></summary>
  <dl>
    <dt>What is Terraform?</dt>
    <dd><p>Terraform is an infrastructure-as-code tool that lets you define resources in human-readable configuration files.</p><p><a href="https://developer.hashicorp.com/terraform/intro">Learn more about Terraform</a>.</p></dd>
    <dt>What is the Terraform Registry?</dt>
    <dd><p>The Terraform Registry is a public collection of resource packages that you can use to create your infrastructure. The Registry has code maintained by third-party developers, including the three major cloud providers (AWS, Azure, and GCP).</p><p><a href="https://registry.terraform.io/?product_intent=terraform">Explore the Terraform Registry</a>.</p></dd>
    <dd><p>The <code>azurerm</code> provider is a code package that Microsoft maintains and hosts in the Terraform Registry. This provider lets you create different resources in Azure.</p><p><a href="https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs">See the <code>azurerm</code> documentation</a> to learn more about how to create different resources.</p></dd>
    <dt>How does Terraform keep track of my environment's configuration?</dt>
    <dd><p>Terraform uses your environment's state to keep track of its real-world configuration. It keeps this state in a file named <code>terraform.tfstate</code>.</p><p><a href="https://developer.hashicorp.com/terraform/language/state">Learn more about how Terraform manages your environment's state</a>.</p></dd>
  </dl>
</details>

<details>
  <summary><strong>Web apps and Azure</strong></summary>
  <dl>
    <dt>What is a web app?</dt>
    <dd>{{ site.data.azure-web-app-with-terraform.definitions.web-app | markdownify }}</dd>
    <dt>What is an Azure resource group?</dt>
    <dd>{{ site.data.azure-web-app-with-terraform.definitions.resource-group | markdownify }}</dd>
    <dt>What is a virtual network?</dt>
    <dd>{{ site.data.azure-web-app-with-terraform.definitions.virtual-network | markdownify }}</dd>
    <dt>Why do I need a network security group?</dt>
    <dd>A network security group keeps your network safe from threats over the public internet. <a href="https://learn.microsoft.com/en-us/azure/virtual-network/network-security-groups-overview">Learn more about network security
groups</a>.</dd>
    <dt>Why do I need to add a network security rule to allow inbound traffic on port 22?</dt>
    <dd>You must allow inbound traffic on port 22 before you can connect to a virtual machine (VM) in your network. <a href="https://learn.microsoft.com/en-us/azure/virtual-machines/linux-vm-connect?tabs=Linux">Learn more about how to connect to a VM</a>.</dd>
  </dl>
</details>


## Learn more

- [Azure Vnet concepts and best practices](https://learn.microsoft.com/en-us/azure/virtual-network/concepts-and-best-practices)
- [Network security groups overview](https://learn.microsoft.com/en-us/azure/virtual-network/network-security-groups-overview)
- [How network security groups filter network traffic](https://learn.microsoft.com/en-us/azure/virtual-network/network-security-group-how-it-works)
- [Manage Azure resource groups by using the Azure portal](https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/manage-resource-groups-portal)
- [`azurerm` provider in Terraform Registry](https://registry.terraform.io/providers/hashicorp/azurerm/4.11.0)
- [Azure Provider: Authenticating using the Azure CLI](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/guides/azure_cli)
- [Authenticate to Azure using Azure CLI](https://learn.microsoft.com/en-us/cli/azure/authenticate-azure-cli)

