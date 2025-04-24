name: Auto Commit x5

on:
  schedule:
    - cron: '0 6 * * *'   # premier commit à 6h
    - cron: '0 9 * * *'   # deuxième commit à 9h
    - cron: '0 12 * * *'  # troisième commit à 12h
    - cron: '0 15 * * *'  # quatrième commit à 15h
    - cron: '0 18 * * *'  # cinquième commit à 18h
  workflow_dispatch:

jobs:
  auto-commit:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout repo
        uses: actions/checkout@v3

      - name: Update log
        run: |
          echo "Ping at $(date)" >> activity.log

      - name: Commit and push
        run: |
          git config --global user.name "William Le Gall"
          git config --global user.email "william@example.com" # change ton mail ici
          git add activity.log
          git commit -m "Auto commit at $(date)" || echo "Nothing to commit"
          git push
