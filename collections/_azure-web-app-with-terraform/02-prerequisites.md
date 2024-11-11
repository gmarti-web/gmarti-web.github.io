---
title: Prerequisites
permalink: /azure-web-app-with-terraform/prerequisites/
date: 2024-11-09
last_modified_at: 2024-11-10
collection: azure-web-app-with-terraform
order: 2
excerpt: Install the needed software and set up your environment.
---

## Create a free Azure account

{% include create-azure-account.html %}

## Set up the Azure CLI

{% include login-to-azure-cli.html download=true %}

## Set up a Terraform project

### Install the Terraform package

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

    {% include figure popup=true image_path="/assets/images/terraform-download-finish.png" alt="terraform-download-finish" %}

### Install the Terraform VS Code extensions

1. Open VS Code and select the **Extensions** icon.

    {% include figure popup=true image_path="/assets/images/terraform-vs-code-extension-icon.png" alt="terraform-vs-code-extension-icon" %}

1. Search for **Terraform**.
1. From the search results, find the extension published by HashiCorp.
1. Select **Install**.

    {% include figure popup=true image_path="/assets/images/terraform-vs-code-extension-install.png" alt="terraform-vs-code-extension-install" %}

    A new window opens in VS Code.

If you see the **Uninstall** button in the new window, you've successfully installed the Terraform extension.

{% include figure popup=true image_path="/assets/images/terraform-vs-code-extension-finish.png" alt="terraform-vs-code-extension-finish" %}

### Explore the Terraform Registry

Explanation TBD

1. Go to the [Terraform Registry](https://registry.terraform.io/?product_intent=terraform).
1. Search for the resource you want to use.

    This tutorial uses the [azurerm](https://registry.terraform.io/providers/hashicorp/azurerm/latest) provider.
    {: .notice--primary }
