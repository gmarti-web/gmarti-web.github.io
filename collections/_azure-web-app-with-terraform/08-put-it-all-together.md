---
title: Deploy your resources with Terraform
permalink: /azure-web-app-with-terraform/deploy-your-resources/
last_modified_at: 2024-11-15
order: 8
excerpt: Deploy your resources to create a web app.
---

After you've defined your resources, Terraform creates them for you in Azure. It determines in what order resources need to be created. It tracks your resources for you, so you can change them at any time without starting over.

This page describes how to review your Terraform plan and deploy your resources.

## Run the Terraform command

1. In your terminal, run the following command:

    ```console
    terraform plan
    ```

    This command tells you how Terraform will build your infrastructure.

    {% include tip-notice.html content="Always review the plan before you create or edit resources. This is your chance to catch any misconfigurations that might harm or accidentally delete your resources." %}

1. After you review the plan, run the following command:

    ```console
    terraform apply -auto-approve
    ```

    This creates your infrastructure. This may take a few minutes.

Confirmation screenshot TBD.

## Troubleshooting

TBD

## Learn more

TBD

