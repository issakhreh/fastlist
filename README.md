# .github/workflows/docs-builder.yml
name: 📘 Markdown to HTML Docs Builders

on:
  push:
    branches: [main]

jobs:
  build-docs:
    runs-on: ubuntu-latest

    steps:
    - name: 📥 Checkout repository
      uses: actions/checkout@v3

    - name: 🛠 Setup Node.js
      uses: actions/setup-node@v3
      with:
        node-version: '18'

    - name: 📦 Install markdown converte
      run: |
        npm install -g markdown-to-html

    - name: 🏗 Convert Markdown to HTML
      run: |
        mkdir -p html
        for file in docs/*.md; d
          markdown-to-html "$file" > "html/$(basename "$file" .md).html"
        done

    - name: 🚀 Deploy to GitHub Pages
      uses: peaceiris/actions-gh-pages@v3
      with:
        github_token: ${{ secrets.GITHUB_TOKEN }}
        publish_dir: ./html
