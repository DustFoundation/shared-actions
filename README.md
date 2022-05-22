# shared-actions

- [Terraform Apply](#terraform-apply) – Terraform apply
- [Terraform Plan](#terraform-plan) – Terraform plan
- [Serverless Deploy (Node.js)](#serverless-deploy-nodejs) – Serverless deploy for Node.js apps
- [CI (Node.js)](#ci-nodejs) – Test & Lint for Node.js apps
- [Publish (NPM)](#publish-npm) – Test, Build & Publish to NPM registry for Node.js apps
- [Create Release](#create-release) – Create GitHub release

---

## Terraform Apply

| OPTION            | TYPE                                                     |
|-------------------|----------------------------------------------------------|
| working-directory | ?string (default: `tf`)                                  |
| apply-command     | ?string (default: `terraform init` \| `terraform apply`) |

```yaml
jobs:
  apply:
    uses: DustFoundation/shared-actions/.github/workflows/terraform-apply.yml@v1.1.1
    secrets:
      aws-id: ${{ secrets.AWS_ID_DEV }}
      aws-secret: ${{ secrets.AWS_SECRET_DEV }}
      git-read-key: ${{ secrets.GIT_READ_KEY }}
```

- If you have environments in folders:

```yaml
    with:
      working-directory: tf/_env/dev
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

| OPTION            | TYPE                    |
|-------------------|-------------------------|
| working-directory | ?string (default: `tf`) |

```yaml
jobs:
  plan:
    uses: DustFoundation/shared-actions/.github/workflows/terraform-plan.yml@v1.1.1
    secrets:
      aws-id: ${{ secrets.AWS_ID_DEV }}
      aws-secret: ${{ secrets.AWS_SECRET_DEV }}
      git-read-key: ${{ secrets.GIT_READ_KEY }}
```

- If you have environments in folders:

```yaml
    with:
      working-directory: tf/_env/dev
```

---

## Serverless Deploy (Node.js)

| OPTION       | TYPE                             |
|--------------|----------------------------------|
| stage        | enum: `dev` \| `stage` \| `prod` |
| node-version | ?number (default: `16`)          |

```yaml
jobs:
  deploy:
    uses: DustFoundation/shared-actions/.github/workflows/serverless-deploy-nodejs.yml@v1.1.1
    with:
      stage: dev
    secrets:
      aws-id: ${{ secrets.AWS_ID_DEV }}
      aws-secret: ${{ secrets.AWS_SECRET_DEV }}
      git-read-key: ${{ secrets.GIT_READ_KEY }}
```

---

## CI (Node.js)

| OPTION       | TYPE                    |
|--------------|-------------------------|
| node-version | ?number (default: `16`) |

```yaml
jobs:
  ci:
    uses: DustFoundation/shared-actions/.github/workflows/ci-nodejs.yml@v1.1.1
    secrets:
      aws-id: ${{ secrets.AWS_ID_DEV }}
      aws-secret: ${{ secrets.AWS_SECRET_DEV }}
      git-read-key: ${{ secrets.GIT_READ_KEY }}
```

---

## Publish (NPM)

| OPTION       | TYPE                    |
|--------------|-------------------------|
| node-version | ?number (default: `16`) |

```yaml
jobs:
  publish:
    uses: DustFoundation/shared-actions/.github/workflows/publish-npm.yml@v1.1.1
    secrets:
      npm-publish-token: ${{ secrets.NPM_PUBLISH_TOKEN }}
```

---

## Create Release

| OPTION     | TYPE                       |
|------------|----------------------------|
| prerelease | ?boolean (default: `true`) |

```yaml
jobs:
  release:
    uses: DustFoundation/shared-actions/.github/workflows/create-release.yml@v1.1.1
```

---
