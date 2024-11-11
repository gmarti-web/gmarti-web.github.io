---
title: Prerequisites
permalink: /azure-web-app-with-terraform/prerequisites/
last_modified_at: 2024-11-09
collection: azure-web-app-with-terraform
order: 2
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

    {% include figure popup=true image_path="/assets/images/terraform-download-finish.png" alt="terraform-download-finish" caption="Confirm the Terraform installation was successful" %}

### Install the Terraform VS Code extensions

### Explore the Terraform registry
