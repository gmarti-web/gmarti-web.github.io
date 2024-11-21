---
title: Connect to Azure with Terraform
permalink: /azure-web-app-with-terraform/connect-to-azure/
last_modified_at: 2024-11-15
order: 3
excerpt: Set up your Terraform workspace and connect to Azure.
---

The [azurerm documentation](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs#authenticating-to-azure) in the Terraform Registry lists different ways to authenticate to Azure. In this tutorial, we'll authenticate with the Azure CLI. If you want to automate this process, you authenticate with a service principal or managed service identity instead.

This page describes how to log into the Azure CLI and set up your `azurerm` Terraform provider.

## Log into the Azure CLI

{% include login-to-azure-cli.html %}

## Create a `providers.tf` file

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

## Troubleshooting 

TBD

## Learn more

TBD
