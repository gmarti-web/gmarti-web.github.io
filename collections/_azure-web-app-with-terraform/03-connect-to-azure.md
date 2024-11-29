---
title: Connect to Azure with Terraform
permalink: /azure-web-app-with-terraform/connect-to-azure/
last_modified_at: 2024-11-24
order: 3
excerpt: Set up your Terraform workspace and connect to Azure.
---

In this tutorial, we'll authenticate to the Terraform `azurerm` provider with
the Azure CLI.

{%- capture tip-content -%} The [azurerm
documentation](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs#authenticating-to-azure)
in the Terraform Registry lists different ways to authenticate to Azure. If you
want to automate this process, authenticate with a service principal or managed
service identity instead. {% endcapture %}

{% include tip-notice.html content=tip-content %}

This page describes how to log into the Azure CLI and set up your `azurerm`
Terraform provider.

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

## Initialize your Terraform workspace

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

## Learn more

- [`azurerm` provider in Terraform Registry](https://registry.terraform.io/providers/hashicorp/azurerm/4.11.0)
- [Azure Provider: Authenticating using the Azure CLI](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/guides/azure_cli)
- [Authenticate to Azure using Azure CLI](https://learn.microsoft.com/en-us/cli/azure/authenticate-azure-cli)

