Examples
```yaml
jobs:
  apply:
    uses: DustFoundation/shared-actions/.github/workflows/terraform-apply.yml@v0.0.4
    secrets:
      aws-id: ${{ secrets.AWS_ID_DEV }}
      aws-secret: ${{ secrets.AWS_SECRET_DEV }}
      git-read-key: ${{ secrets.GIT_READ_KEY }}
```
If you have a script for configure backend
```yaml
jobs:
  apply:
    uses: DustFoundation/shared-actions/.github/workflows/terraform-apply.yml@v0.0.4
    with:
      apply-command: ./apply-prod.sh
    secrets:
      aws-id: ${{ secrets.AWS_ID_PROD }}
      aws-secret: ${{ secrets.AWS_SECRET_PROD }}
      git-read-key: ${{ secrets.GIT_READ_KEY }}
```
