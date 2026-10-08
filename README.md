InterSystems Demo Deployment
===

- [Usage](#usage)
- [How it deploys](#how-it-deploys)

Usage
==

In your repository create file `.github/workflows/deploy.yml` with content. Replace `<name-of-demo>` with the domain name, which will be used before `.demo.community.intersystems.com`. Ask for deployment key and set it to secrets as `SERVICE_ACCOUNT_KEY`

```yaml
name: Demo Deploy

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
      ## Optional
      # memory: 1Gi
      # port: 8081
      # persistence: true
      # namespace: demo
    secrets:
      SERVICE_ACCOUNT_KEY: ${{ secrets.SERVICE_ACCOUNT_KEY }}
      ## Optional
      # CUSTOM_VARS_LIST: "var1=${{ secrets.CUSTOM_VAR1 }},var2=value2,..."
```

How it deploys
==

The workflow builds your repository's `Dockerfile`, pushes the image to Artifact Registry and installs it on the `demo` GKE cluster as a Helm release of the `iris-app` chart (one IRIS instance). The release is exposed at `https://<name-of-demo>.demo.community.intersystems.com` through an nginx Ingress, with TLS from cert-manager and DNS from external-dns.

- `persistence: false` (default): no volumes. Data written at runtime is lost whenever the pod restarts or is redeployed.
- `persistence: true`: IRIS data (`ISC_DATA_DIRECTORY=/isc/data`), WIJ and journals are kept on 10Gi persistent volumes.
