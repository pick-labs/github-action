# Pick Bot

 Guide to use the pick bot in the GitHub Actions workflow.

> [!IMPORTANT]  
> Only support the **Squash** pull request.

## Permissions

Go to create personal access token in the GitHub settings and select the following permissions:
> Your Avatar > Settings > Developer settings > Personal access tokens > Generate new token

- [x] repo 
- [x] admin:org

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
      - uses: actions/checkout@v4
        fetch-depth: 0 # get all history
        
      - name: Pick bot
        uses: pick-labs/github-action@v1
        with:
          # Your GitHub token
          token: ${{ secrets.BOT_TOKEN }}  
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
