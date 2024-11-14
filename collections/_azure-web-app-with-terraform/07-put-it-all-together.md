---
title: Put it all together
permalink: /azure-web-app-with-terraform/put-it-all-together/
date: 2024-11-10
last_modified_at: 2024-11-11
order: 7
excerpt: Link your services together to create a web app.
---

## Background

TBD

## Connect the services

1. Open the `main.tf` file.
1. Add the following Terraform code to the bottom of the file:

    ```hcl
        resource "azurerm_subnet" "subnet" {
            name                 = "internalsubnet"
            resource_group_name  = azurerm_resource_group.rg.name
            virtual_network_name = azurerm_virtual_network.vnet.name
            address_prefixes     = ["10.0.2.0/24"]
        }

        resource "azurerm_mssql_virtual_network_rule" "vnetrule" {
            name      = "sql-vnet-rule"
            server_id = azurerm_mssql_server.mssql_server.id
            subnet_id = azurerm_subnet.subnet.id
        }
    ```

1. In the `azurerm_network_interface` resource, add the following line to the `ip_configuration` block:

    ```hcl
    subnet_id = azurerm_subnet.subnet.id
    ```

1. Save the `main.tf` file.

## Run the Terraform command

1. In your terminal, run the following command:

    ```console
    terraform plan
    ```

    This command tells you how Terraform will build your infrastructure. Always review the plan before creating resources.

1. After you review the plan, run the following command:

    ```console
    terraform apply -auto-approve
    ```

    This creates your infrastructure. This may take a few minutes.

Confirmation screenshot TBD.

## Troubleshooting

TBD

## Learn more

TBD
