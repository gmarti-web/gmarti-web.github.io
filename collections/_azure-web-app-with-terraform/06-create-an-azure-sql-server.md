---
title: Create an Azure SQL server
permalink: /azure-web-app-with-terraform/create-an-azure-sql-server/
date: 2024-11-10
last_modified_at: 2024-11-11
order: 6
excerpt: TBD
---

## Background

TBD

## Create a SQL server

1. Open the `main.tf` file.
1. Add the following Terraform code to the bottom of the file:

    ```hcl
    resource "azurerm_mssql_server" "mssql_server" {
        name                         = "azure-web-app-mssqlserver"
        resource_group_name          = azurerm_resource_group.rg.name
        location                     = azurerm_resource_group.rg.location
        version                      = "12.0"
        administrator_login          = "Example-Administrator"
        administrator_login_password = "myp@sswoRD11!"
        minimum_tls_version          = "1.2"
    }
    ```

1. Save the `main.tf` file.

## Troubleshooting

TBD

## Learn more

TBD
