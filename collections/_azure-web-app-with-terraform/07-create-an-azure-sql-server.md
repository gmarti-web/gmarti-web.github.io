---
title: Create an Azure SQL server
permalink: /azure-web-app-with-terraform/create-an-azure-sql-server/
last_modified_at: 2024-11-27
order: 7
excerpt: Create an Azure SQL server with Terraform.
---

An Azure SQL server is a relational database management system (RDBMS). It saves data in tables that can be filtered and sliced with SQL queries. Our web app needs a SQL server to save and retrieve data from users.

This page describes how to create an Azure SQL server and connect it to our virtual network's subnet.

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

1. Save the `main.tf` file.

## Learn more

TBD

