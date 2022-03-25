# shared-actions

## Terraform apply
Example
```yaml
jobs:
  apply:
    uses: DustFoundation/shared-actions/.github/workflows/terraform-apply.yml@v0.0.4
    secrets:
      aws-id: ${{ secrets.AWS_ID_DEV }}
      aws-secret: ${{ secrets.AWS_SECRET_DEV }}
      git-read-key: ${{ secrets.GIT_READ_KEY }}
```
