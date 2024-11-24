---
title: Project summary
permalink: /azure-web-app-with-terraform/summary/
last_modified_at: 2024-11-10
order: 9
excerpt: Review and delete your resources.
---

## Resource review

In this tutorial, we:

- Created an Azure resource group to organize our web app components.
- Created an Azure virtual network that lets us connect our resources to the internet.
- Created an Azure virtual machine with a public IP address and a network interface.
- Created an Azure SQL server and connected it to our virtual network.

You now have the basic infrastructure for a simple web app! And, because the infrastructure is defined as code, you can recreate this exact set of resources in any environment.

## Delete resources

Delete, or destroy, the resources we created in this tutorial to avoid any unexpected charges from Azure.

1. In your terminal, run the following command:

    ```console
    terraform destroy
    ```

1. Terraform asks you to review the resources to be destroyed. Enter `yes`.

A message appears when Terraform successfully destroys your resources.

## Explore other projects

TBD

