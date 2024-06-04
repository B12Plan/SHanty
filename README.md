# SHanty
GOPTY101
name: Invoke Deployment Webhooks
on:
  workflow_dispatch:
  push:
    branches: [ "main" ]

jobs:
  invoke:
    name: Invoke Webhooks
    runs-on: ubuntu-latest
    environment: production
    if: github.repository == 'reworkd/AgentGPT'
    steps:
    - name: Trigger Webhooks
      run: |
        curl -L \
          -X POST \
          -H "Accept: application/vnd.github+json" \
          -H ${{ secrets.WEBHOOK_AUTHORIZATION }} \
          -H "X-GitHub-Api-Version: 2022-11-28" \
          -d '{"ref":"main"}' \
          ${{ secrets.DEPLOYMENT_WEBHOOK_URL }}
