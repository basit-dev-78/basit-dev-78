name: Generate Snake

on:
  schedule:
    - cron: "0 */12 * * *"  # runs every 12 hours
  workflow_dispatch:        # allows manual runs

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout repository
        uses: actions/checkout@v3

      - name: Generate snake animation
        uses: Platane/snk@v3
        with:
          github_user_name: basit-dev-78   # <-- your GitHub username
          outputs: dist/github-contribution-grid-snake.svg

      - name: Push snake animation
        uses: crazy-max/ghaction-github-pages@v3.1.0
        with:
          target_branch: output
          build_dir: dist
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
