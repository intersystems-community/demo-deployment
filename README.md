InterSystems Dev Cloud Deployment
===

Usage
==

In your repository create file `.github/workflows/deploy.yml` with content. Replace `<name-of-demo>` with the domain name, which will be used before `.sandbox.developer.intersystems.com`. Ask for deployment key and set it to secrets as `SERVICE_ACCOUNT_KEY`

```yaml
name: Dev Cloud Deploy

on:
  push:
    branches:
    - master
    - main
  workflow_dispatch:

jobs:
  deploy:
    uses: intersystems-community/cloud-deployment/.github/workflows/deployment.yml@dev-cloud-deployment
    with:
      name: <name-of-demo>
      ## Optional
      # memory: 1Gi
      # port: 8081
    secrets:
      SERVICE_ACCOUNT_KEY: ${{ secrets.SERVICE_ACCOUNT_KEY }}
      ## Optional
      # CUSTOM_VARS_LIST: "var1=${{ secrets.CUSTOM_VAR1 }},var2=value2,..."
```
