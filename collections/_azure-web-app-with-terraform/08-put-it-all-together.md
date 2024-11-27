---
title: Deploy your resources with Terraform
permalink: /azure-web-app-with-terraform/deploy-your-resources/
last_modified_at: 2024-11-27
order: 8
excerpt: Deploy your resources to create a web app.
---

Terraform uses the definitions in the `maint.tf` file to create resources in Azure. It determines in what order resources need to be created. And, it tracks your resources for you, so you can change them in the `main.tf` file at any time without starting from scratch.

This page describes how to review your Terraform plan and deploy your resources.

## Run the Terraform command

1. In your terminal, run the following command:

    ```console
    terraform plan
    ```

    This command tells you how Terraform will build your infrastructure. It tallys up how many resources your Terraform code will add, change, or destroy.

    {% include figure
      popup=true
      image_path="/assets/images/terraform-plan.png"
      alt="terraform-plan"
      caption="`terraform plan` output"
    %}

    {% include tip-notice.html content="Always review the plan before you create or edit resources. This is your chance to catch any misconfigurations that might harm or accidentally delete your resources." %}

1. After you review the plan, run the following command:

    ```console
    terraform apply -auto-approve
    ```

    The command asks you to confirm. To do so, enter `yes`.

    {% include figure
      popup=true
      image_path="/assets/images/terraform-apply-confirm.png"
      alt="terraform-apply-confirm"
      caption="`terraform apply` confirmation message"
    %}

    This creates your infrastructure. This may take a few minutes.

The results are displayed in your terminal.

{% include figure
  popup=true
  image_path="/assets/images/terraform-apply-complete.png"
  alt="terraform-apply-complete"
  caption="`terraform apply` completion message"
%}

Your resources are ready to use in Azure. See your new resource group in the [Azure portal](https://azure.portal.com).

{% include figure
  popup=true
  image_path="/assets/images/azure-resources.png"
  alt="azure-resources"
  caption="Azure resource group details"
%}

## Learn more

TBD

