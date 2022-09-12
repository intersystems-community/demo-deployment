InterSystems Demo Deployment action
===


Usage
==

```yaml
on:
  push:
    branches:
      - master
      - main
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Deploy Demo
        if: github.event.repository.fork == false && github.event.repository.is_template == false
        uses: intersystems-community/demo-deployment@master
        with:
          name: demo
```
