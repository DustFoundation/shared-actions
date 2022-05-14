# shared-actions

- [Terraform Apply](#terraform-apply) – Terraform apply
- [Terraform Plan](#terraform-plan) – Terraform plan
- [Serverless Deploy (Node.js)](#serverless-deploy-nodejs) – Serverless deploy for Node.js services
- [Pre-release](#pre-release) – Create pre-release for stage/prod deployment

---

## Terraform Apply

### Basic Usage

```yaml
jobs:
  apply:
    uses: DustFoundation/shared-actions/.github/workflows/terraform-apply.yml@v0.0.5
    secrets:
      aws-id: ${{ secrets.AWS_ID_DEV }}
      aws-secret: ${{ secrets.AWS_SECRET_DEV }}
      git-read-key: ${{ secrets.GIT_READ_KEY }}
```

### If you have environments in folders

```yaml
jobs:
  apply:
    uses: DustFoundation/shared-actions/.github/workflows/terraform-apply.yml@v0.0.5
    with:
      working-directory: tf/_env/dev
    secrets:
      aws-id: ${{ secrets.AWS_ID_DEV }}
      aws-secret: ${{ secrets.AWS_SECRET_DEV }}
      git-read-key: ${{ secrets.GIT_READ_KEY }}
```

### If you have a script for configure backend

```yaml
jobs:
  apply:
    uses: DustFoundation/shared-actions/.github/workflows/terraform-apply.yml@v0.0.5
    with:
      apply-command: ./apply-stage.sh
    secrets:
      aws-id: ${{ secrets.AWS_ID_STAGE }}
      aws-secret: ${{ secrets.AWS_SECRET_STAGE }}
      git-read-key: ${{ secrets.GIT_READ_KEY }}
```

### If you want to define terraform command for each stage

```yaml
jobs:
  apply:
    uses: DustFoundation/shared-actions/.github/workflows/terraform-apply.yml@v0.0.5
    with:
      apply-command: |
        terraform init -backend-config="key=stage/frontend.tfstate"
        terraform apply -auto-approve -var-file stage.tfvars
    secrets:
      aws-id: ${{ secrets.AWS_ID_STAGE }}
      aws-secret: ${{ secrets.AWS_SECRET_STAGE }}
      git-read-key: ${{ secrets.GIT_READ_KEY }}
```

---

## Terraform Plan

### Basic Usage

```yaml
jobs:
  plan:
    uses: DustFoundation/shared-actions/.github/workflows/terraform-plan.yml@v0.0.5
    secrets:
      aws-id: ${{ secrets.AWS_ID_DEV }}
      aws-secret: ${{ secrets.AWS_SECRET_DEV }}
      git-read-key: ${{ secrets.GIT_READ_KEY }}
```

### If you have environments in folders

```yaml
jobs:
  plan:
    uses: DustFoundation/shared-actions/.github/workflows/terraform-plan.yml@v0.0.5
    with:
      working-directory: tf/_env/dev
    secrets:
      aws-id: ${{ secrets.AWS_ID_DEV }}
      aws-secret: ${{ secrets.AWS_SECRET_DEV }}
      git-read-key: ${{ secrets.GIT_READ_KEY }}
```

---

## Serverless Deploy (Node.js)

### Basic Usage

```yaml
jobs:
  deploy:
    uses: DustFoundation/shared-actions/.github/workflows/serverless-deploy-nodejs.yml@v0.0.5
    with:
      stage: dev
    secrets:
      aws-id: ${{ secrets.AWS_ID_DEV }}
      aws-secret: ${{ secrets.AWS_SECRET_DEV }}
      git-read-key: ${{ secrets.GIT_READ_KEY }}
```

### Custom Node.js version (default is 16)

```yaml
jobs:
  deploy:
    uses: DustFoundation/shared-actions/.github/workflows/serverless-deploy-nodejs.yml@v0.0.5
    with:
      stage: dev
      node-version: 16
    secrets:
      aws-id: ${{ secrets.AWS_ID_DEV }}
      aws-secret: ${{ secrets.AWS_SECRET_DEV }}
      git-read-key: ${{ secrets.GIT_READ_KEY }}
```

---

## Pre-release

### Basic Usage

```yaml
jobs:
  pre-release:
    uses: DustFoundation/shared-actions/.github/workflows/pre-release.yml@v0.0.5
```

---
