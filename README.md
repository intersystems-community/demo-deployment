InterSystems Demo Deployment
===

Usage
==

In your repository create file `.github/workflows/deploy.yml` with content. Replace `<name-of-demo>` with the domain name, which will be used before `.demo.community.intersystems.com`. Ask for deployment key and set it to secrets as `SERVICE_ACCOUNT_KEY`

```yaml
name: Cloud Run Deploy

on:
  push:
    branches:
    - master
    - main
  workflow_dispatch:

jobs:
  deploy:
    uses: intersystems-community/demo-deployment/.github/workflows/deployment.yml@master
    with:
      name: <name-of-demo>
    secrets:
      SERVICE_ACCOUNT_KEY: ${{ secrets.SERVICE_ACCOUNT_KEY }}
```
