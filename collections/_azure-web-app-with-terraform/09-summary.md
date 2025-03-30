---
title: Project summary
permalink: /azure-web-app-with-terraform/summary/
date: 2024-11-29
last_modified_at: 2025-03-30
order: 9
excerpt: Review and delete your resources.
---

## Resource review

In this tutorial, we:

- Created an Azure resource group to organize our web app components.
- Created an Azure virtual network that lets us connect our resources to the internet.
- Created an Azure virtual machine with a public IP address and a network interface.
- Created an Azure SQL server and connected it to our virtual network.

You now have the basic infrastructure for a simple web app! And, because the
infrastructure is defined as code, you can recreate this exact set of resources
in any environment with the same configuration script.

## Delete resources

Delete, or destroy, the resources we created in this tutorial to avoid any
unexpected Azure charges.

1. In your terminal, run the following command:

    ```console
    terraform destroy
    ```

    This command tells you which resources Terraform will destroy.

1. Enter `yes` to confirm that you want to destroy these resources.

    {% include figure
      popup=true
      image_path="/assets/images/terraform-destroy-confirm.png"
      alt="terraform-destroy-confirm"
      caption="`terraform destroy` confirmation message"
    %}

A message appears when Terraform successfully destroys your resources.

{% include figure
  popup=true
  image_path="/assets/images/terraform-destroy-complete.png"
  alt="terraform-destroy-complete"
  caption="`terraform apply` completion message"
%}

## Explore other projects

- [Learn about Terraform modules](https://developer.hashicorp.com/terraform/language/modules)
- [15+ Terraform real-time project examples](https://www.projectpro.io/article/terraform-projects-examples/621)

