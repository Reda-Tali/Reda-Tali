<h1 align="center">Hi 👋, I'm Reda</h1>
<h3 align="center">I’m a motivated student driven by learning, discipline, and continuous improvement. This GitHub reflects my commitment to building a strong foundation through consistent practice and curiosity. I focus on understanding things deeply, improving step by step, and taking my studies seriously. 📚 Always learning 🚀 Focused and ambitious</h3>

name: Generate snake animation

on:
  schedule: # execute every 12 hours
    - cron: "* */12 * * *"

  workflow_dispatch:

  push:
    branches:
    - main

jobs:
  generate:
    permissions:
      contents: write
    runs-on: ubuntu-latest
    timeout-minutes: 5

    steps:
      - name: generate snake.svg
        uses: Platane/snk/svg-only@v3
        with:
          github_user_name: ${{ github.repository_owner }}
          outputs: dist/snake.svg?palette=github-dark


      - name: push snake.svg to the output branch
        uses: crazy-max/ghaction-github-pages@v3.1.0
        with:
          target_branch: output
          build_dir: dist
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
