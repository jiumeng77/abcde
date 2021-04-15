
name: ziye-sync
on:
  schedule:
    - cron: '1 */3 * * *'
  workflow_dispatch:
  watch:
    types: started
  repository_dispatch:
    types: sync-ziye888-JavaScript
jobs:
  repo-sync:
    env:
      PAT: ${{ secrets.PAT }} 
    runs-on: ubuntu-latest
    if: github.event.repository.owner.id == github.event.sender.id
    steps:
      - uses: actions/checkout@v2
        with:
          persist-credentials: false

      - name: sync ziye888-JavaScript
        uses: repo-sync/github-sync@v2
        if: env.PAT
        with:
          source_repo: "https://github.com/ziye888/JavaScript.git"
          source_branch: "main"
          destination_branch: "ZIYE2"
          github_token: ${{ secrets.PAT }}
