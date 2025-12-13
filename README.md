name: Generate contribution snake

on:
  schedule:
    - cron: '0 0 * * *' # daily at 00:00 UTC (change if you want)
  workflow_dispatch:

permissions:
  contents: write

jobs:
  generate:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout repository
        uses: actions/checkout@v4

      - name: Setup Node.js
        uses: actions/setup-node@v4
        with:
          node-version: '18'

      - name: Generate contribution snake SVG
        run: |
          mkdir -p output
          npx @platane/github-contribution-grid-snake \
            --username "Clarkky1" \
            --output ./output/github-contribution-grid-snake.svg \
            --square 12 \
            --theme standard

      - name: Commit and push generated SVG
        uses: EndBug/add-and-commit@v9
        with:
          author_name: github-actions
          author_email: github-actions@github.com
          message: "chore: update contribution snake"
          add: 'output/github-contribution-grid-snake.svg'
          push: true
````markdown name=README.md url=https://github.com/Clarkky1/Introduction/blob/main/README.md
```html
# Hi, I'm Kin Clark 👋

### My Core Tech Stack

<p align="left">
  <img src="https://skillicons.dev/icons?i=flutter,dart,supabase,firebase,postgresql,nodejs,typescript,javascript" />
</p>

<!-- Contribution grid snake (generated SVG) -->
<!-- The workflow will create output/github-contribution-grid-snake.svg; change 'main' in the URL if your default branch differs -->
<img alt="github contribution grid snake animation" src="https://raw.githubusercontent.com/Clarkky1/Introduction/main/output/github-contribution-grid-snake.svg" style="max-width:100%;">
