---
title: Prerequisites
permalink: /azure-web-app-with-terraform/prerequisites/
last_modified_at: 2024-11-15
order: 2
---

To follow this tutorial, you need:

- An Azure account
- The Azure CLI program
- The Terraform CLI program

Optionally, you may want to save your work in a [GitHub repository](https://github.com/), as well.

This page describes how to set up and install the necessary applications.

## Create a free Azure account

{% include create-azure-account.html %}

## Set up the Azure CLI

{% include login-to-azure-cli.html download=true %}

## Install the Terraform CLI

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

## Install the Terraform VS Code extensions

1. Open VS Code and select the **Extensions** icon.

    {% include figure
      popup=true
      image_path="/assets/images/terraform-vs-code-extension-icon.png"
      alt="terraform-vs-code-extension-icon"
    %}

1. Search for **Terraform**.
1. From the search results, find the extension published by HashiCorp.
1. Select **Install**.

    {% include figure
      popup=true
      image_path="/assets/images/terraform-vs-code-extension-install.png"
      alt="terraform-vs-code-extension-install"
    %}

    A new window opens in VS Code.

You've successfully installed the Terraform extension

