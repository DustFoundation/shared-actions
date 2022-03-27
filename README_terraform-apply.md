Examples
```yaml
jobs:
  apply:
    uses: DustFoundation/shared-actions/.github/workflows/terraform-apply.yml@v0.0.5
    secrets:
      aws-id: ${{ secrets.AWS_ID_DEV }}
      aws-secret: ${{ secrets.AWS_SECRET_DEV }}
      git-read-key: ${{ secrets.GIT_READ_KEY }}
```
If you have a script for configure backend
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
If you want to define terraform command for each stage:
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
If you have environments in folders
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
