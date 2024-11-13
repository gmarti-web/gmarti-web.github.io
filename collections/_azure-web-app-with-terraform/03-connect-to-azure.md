---
title: Connect to Azure with Terraform
permalink: /azure-web-app-with-terraform/connect-to-azure/
date: 2024-11-10
last_modified_at: 2024-11-13
order: 3
excerpt: Set up your Terraform workspace and connect to Azure.
---

## Background

TBD

## Create your repository

1. Create a folder called `azure-web-app-with-terraform`.

    ```console
    mkdir azure-web-app-with-terraform
    ```

1. Change directories into that folder.

    ```console
    cd azure-web-app-with-terraform
    ```

1. Open VS Code in this folder.

## Create a `providers.tf` file

1. Instructions on getting Azure subscription ID TBD.
1. Create a new file and enter the following Terraform code:

    ```hcl
    terraform {
        required_providers {
            azurerm = {
            source = "hashicorp/azurerm"
            version = "4.9.0"
            }
        }
    }

    provider "azurerm" {
        features {}
        subscription_id = <YOUR-AZURE-SUBSCRIPTION-ID>
    }
    ```

1. Save this file as `providers.tf`.

    This file defines your Terraform providers. You can define any number of providers in your Terraform project. For this tutorial, we'll use only the `azurerm` provider.

## Initialize your Terraform workspace

In your terminal, run the following command:

```console
terraform init
```

Confirmation TBD

## Create a resource group

Explain how resource group holds all our other components TBD.

1. Create a new file and enter the following Terraform code:

    ```hcl
    resource "azurerm_resource_group" "rg" {
        name     = "azure-web-app-with-terraform-rg"
        location = "westus2"
    }
    ```

1. Save this file as `main.tf`.

    We'll create the rest of the infrastructure for this tutorial in this file.

## Troubleshooting 

TBD

## Learn more

TBD
