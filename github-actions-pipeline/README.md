[![LinkedIn](https://img.shields.io/badge/Connect%20with%20me%20on-LinkedIn-blue.svg)](https://www.linkedin.com/in/rohit-rawat-7383091a7/)
[![GitHub](https://img.shields.io/badge/GitHub-Follow-black?style=for-the-badge&logo=github)](https://github.com/RohitRawat891997)
[![Docker](https://img.shields.io/badge/Docker-Profile-2496ED?style=for-the-badge&logo=docker&logoColor=white)](https://hub.docker.com/u/rohitrawat891997)

---

# 🚀 How to Setup the Pipeline and Credentials

## 🔐 Prerequisites

### 1️⃣ Generate Terraform Cloud API Token

* Generate the Terraform Cloud API key.
* Go to **GitHub Repository → Settings → Secrets → Actions**.
* Create a new secret with name:

```
TF_API_TOKEN
```

---

### 2️⃣ AWS Credentials (Only if Terraform Cloud execution mode is local)

Generate AWS credentials and create these secrets in GitHub Actions repository settings:

```
AWS_ACCESS_KEY_ID
AWS_SECRET_ACCESS_KEY
```

---

# ⚙️ Example GitHub Actions Workflow

Below is the workflow configuration for running Terraform actions using GitHub Actions.

```yaml
name: "AWS Terraform workflow"
on:
  workflow_dispatch: # Parameterization to make a selection of apply or destroy.
    inputs:
      TFACTION:
        description: "Terraform Action"
        default: "apply"
        required: true
        type: choice
        options:
         - "apply"
         - "destroy"

permissions:
  contents: 'read'
  id-token: 'write'
jobs:
  aws_action:
    runs-on: ubuntu-latest
    defaults:
      run:
        shell: bash
    name: 'workflow setup'
# Code checkout
    steps:
      - name: Checkout
        uses: actions/checkout@v4
# configure aws credentials for action
      - name: Configure AWS Credentials
        uses: aws-actions/configure-aws-credentials@v4
        with:
          aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
          aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          aws-region: us-east-2
# Setup terraform CLI with TF_API_TOKEN
      - name: Setup Terraform
        uses: hashicorp/setup-terraform@v2
        with:
          terraform_version: 1.8.0
          cli_config_credentials_token: ${{ secrets.TF_API_TOKEN }}
# Initialize terraform
      - name: Terraform Init
        run: terraform  init
        working-directory: tfroot # this is directory where all terraform files are

# Generates an execution plan for Terraform
      - name: Terraform Plan
        run: terraform  plan -input=false
        working-directory: tfroot
# Apply the plan if apply parameter selected during run.
      - name: Terraform Apply
        if: ${{ github.event.inputs.TFACTION == 'apply' }}
        run: terraform  apply --auto-approve -input=false
        working-directory: tfroot
# Destroy the infra if destroy parameter selected during run.
      - name: Terraform Destroy
        if: ${{ github.event.inputs.TFACTION == 'destroy' }}
        run: terraform destroy --auto-approve -input=false
        working-directory: tfroot
```

---

## ▶️ How It Works

* Workflow is triggered manually using **workflow_dispatch**.
* User selects Terraform action (`apply` or `destroy`).
* AWS credentials are configured using GitHub secrets.
* Terraform CLI is setup using Terraform Cloud API token.
* Pipeline runs:

  * `terraform init`
  * `terraform plan`
  * `terraform apply` **OR** `terraform destroy`

---

💡 **Tip:**
Make sure your Terraform code exists inside the `tfroot` directory because workflow uses:

```
working-directory: tfroot
```
# 👨‍💻 Author

**Name:** Rohit Rawat<br>
**GitHub:** [https://github.com/RohitRawat891997](https://github.com/RohitRawat891997)<br>
**LinkedIn:** [https://www.linkedin.com/in/rohit-rawat-7383091a7/](https://www.linkedin.com/in/rohit-rawat-7383091a7/)

---


