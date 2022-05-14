# shared-actions

- [Terraform Apply](#terraform-apply) – Terraform apply
- [Terraform Plan](#terraform-plan) – Terraform plan
- [Serverless Deploy (Node.js)](#serverless-deploy-nodejs) – Serverless deploy for Node.js apps
- [CI (Node.js)](#ci-nodejs) – Test & Lint for Node.js apps
- [Create Release](#create-release) – Create GitHub release

---

## Terraform Apply

| OPTION            | TYPE                                                     | EXAMPLE       |
|-------------------|----------------------------------------------------------|---------------|
| working-directory | ?string (default: `tf`)                                  | `tf/_env/dev` |
| apply-command     | ?string (default: `terraform init` \| `terraform apply`) |               |

```yaml
jobs:
  apply:
    uses: DustFoundation/shared-actions/.github/workflows/terraform-apply.yml@v0.0.6
    secrets:
      aws-id: ${{ secrets.AWS_ID_DEV }}
      aws-secret: ${{ secrets.AWS_SECRET_DEV }}
      git-read-key: ${{ secrets.GIT_READ_KEY }}
```

- If you have a script for configure backend:

```yaml
    with:
      apply-command: ./apply-stage.sh
```

- If you want to define terraform command for each stage

```yaml
    with:
      apply-command: |
        terraform init -backend-config="key=stage/frontend.tfstate"
        terraform apply -auto-approve -var-file stage.tfvars
```

---

## Terraform Plan

| OPTION            | TYPE                    | EXAMPLE       |
|-------------------|-------------------------|---------------|
| working-directory | ?string (default: `tf`) | `tf/_env/dev` |

```yaml
jobs:
  plan:
    uses: DustFoundation/shared-actions/.github/workflows/terraform-plan.yml@v0.0.6
    secrets:
      aws-id: ${{ secrets.AWS_ID_DEV }}
      aws-secret: ${{ secrets.AWS_SECRET_DEV }}
      git-read-key: ${{ secrets.GIT_READ_KEY }}
```

---

## Serverless Deploy (Node.js)

| OPTION       | TYPE   | EXAMPLE                  |
|--------------|--------|--------------------------|
| stage        | enum   | `dev`, `stage` or `prod` |
| node-version | number | 16                       |

```yaml
jobs:
  deploy:
    uses: DustFoundation/shared-actions/.github/workflows/serverless-deploy-nodejs.yml@v0.0.6
    with:
      stage: dev
      node-version: 16
    secrets:
      aws-id: ${{ secrets.AWS_ID_DEV }}
      aws-secret: ${{ secrets.AWS_SECRET_DEV }}
      git-read-key: ${{ secrets.GIT_READ_KEY }}
```

---

## CI (Node.js)

| OPTION       | TYPE   | EXAMPLE |
|--------------|--------|---------|
| node-version | number | 16      |

```yaml
jobs:
  ci:
    uses: DustFoundation/shared-actions/.github/workflows/ci-nodejs.yml@v0.0.6
    with:
      node-version: 16
    secrets:
      aws-id: ${{ secrets.AWS_ID_DEV }}
      aws-secret: ${{ secrets.AWS_SECRET_DEV }}
      git-read-key: ${{ secrets.GIT_READ_KEY }}
```

---

## Create Release

| OPTION     | TYPE                     | EXAMPLE |
|------------|--------------------------|---------|
| prerelease | ?boolean (default: true) | true    |

```yaml
jobs:
  release:
    uses: DustFoundation/shared-actions/.github/workflows/create-release.yml@v0.0.6
```

---
