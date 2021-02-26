# Skpr Package and Deploy Action

A [Github Action](https://docs.github.com/en/actions) for automated deployments to [Skpr](https://www.skpr.com.au)

This action combines all steps into a single Package and Deploy action.

As an alternative, you can use the following _separate_ actions:

- [skpr/setup-action@v1](https://github.com/skpr/setup-action)
- [skpr/info-action@v1](https://github.com/skpr/info-action)
- [skpr/package-action@v1](https://github.com/skpr/package-action)
- [skpr/deploy-action@v1](https://github.com/skpr/deploy-action)
- [skpr/exec-action@v1](https://github.com/skpr/exec-action)

## Inputs

### `env`

**Required** The Skpr environment.

### `package`

**Optional** Whether to package or not. Set to `false` if deploying a pre-packaged app.

### `version`

**Optional** A previously packaged app version.

### `post-deploy`

**Optional** A post-deploy command to run on the environment.

## Outputs

### `url`

The Skpr environment URL.

### `version`

The version to use, based on git describe --tags.


## Example Workflow Usage
```
name: skpr-deploy
on:
  push:
    branches: [master]
env:
  SKPR_USERNAME: ${{ secrets.SKPR_USERNAME }}
  SKPR_PASSWORD: ${{ secrets.SKPR_PASSWORD }}

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout Code
        uses: actions/checkout@v2
        with:
          fetch-depth: 0
      - name: Skpr Package and Deploy
        uses: skpr/package-deploy-action@v1
        with:
          env: dev
          post-deploy: make deploy
```
