# Pick Bot

 Guide to use the pick bot in the GitHub Actions workflow.

## Usage

1. Create a new file `.github/workflows/pick.yml`
```yaml
name: Pick Bot

on:
  workflow_dispatch:

  pull_request:
    types:
      - opened
      - edited
      - reopened
      - closed

jobs:
  pick:
    name: 'Cherry Pick Bot'
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v3
      - name: Pick bot
        uses: pick-labs/github-action@v1
        with:
          token: ${{ secrets.BOT_TOKEN }}  // Your GitHub token
```
2. Create a new file `.pick.yml` in the root of the repository

```yaml
branches:
  - release/xx
  - release/xx
  - release/xx
  - vxx/xx
  - master
```

The robot cherry-pick according to the branch order in the file.
