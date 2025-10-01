# 如何使用GitHub Actions

## Prompt

> how to deploy the app in the flash-cards folder to the apps folder in gh-pages branch for GitHub Pages

## Answer

To deploy the app in the flash-cards folder to the apps folder on the gh-pages branch for GitHub Pages, you should set up a GitHub Actions workflow that copies everything from flash-cards into a subdirectory called apps in your deployment output.

Here’s a workflow example:

```yaml
name: Deploy Flash Cards App

on:
  push:
    branches: [ main ]

jobs:
  deploy:
    runs-on: ubuntu-latest
    permissions:
      contents: write
    steps:
      - name: Checkout code
        uses: actions/checkout@v3

      - name: Prepare output directory
        run: |
          mkdir -p build/apps
          cp -r flash-cards/* build/apps/

      - name: Deploy to GitHub Pages (gh-pages branch)
        uses: JamesIves/github-pages-deploy-action@v4
        with:
          branch: gh-pages
          folder: build
```

This will deploy your app so it’s accessible at `https://<username>.github.io/<repo>/apps/`.

- All files from `flash-cards` will be available under `/apps/` on the published site.
- You can add more folders to `build/` if you want to deploy other apps in the future.

See the workflow file at `.github/workflows/deploy_flash_cards.yaml`.
