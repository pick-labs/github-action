# Pick Bot

 Guide to use the pick bot in the GitHub Actions workflow.

> [!IMPORTANT]  
> Only support the **Squash** pull request.
>
> Please use it only for personal projects, as comments created with a personal access token cannot be modified by others.

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
        with:
          fetch-depth: 0 # get all history
        
      - name: Pick bot
        uses: pick-labs/github-action@v1
        with:
          # Your GitHub token
          token: ${{ secrets.BOT_TOKEN }}  
```
2. Create a new file `.pick.yml` in the root of the repository

```yaml
# Cherry-pick roadmap configuration file .pick.yml
# The robot cherry-pick according to the branch order in the file,
# you can use the `branches` option to specify the branch order.
# If Pr base branch in the middle of the list, the robot will cherry-pick the Pr to the next branch.
branches:
  - release/xx
  - release/xx
  - xx
  - vxx/xx
  - master
```

Example:
- rebot will create markdown comment information to tell you the cherry-pick route ([roadmap example](https://github.com/pick-labs/github-action/pull/9#issuecomment-2059291918)), and you can confirm it or cancel cherry-picking for a certain branch.
- After completion, markdown information will be generated in the PR comments to inform you of the cherry-pick results ([result example](https://github.com/pick-labs/github-action/pull/9#issuecomment-2059292918)).

## Options

See [action.yml](action.yml) for more detail.

| Option      | Required | Description                               | Default   |
|-------------|----------|-------------------------------------------|-----------|
| token       | Y        | Personal access token for the GitHub.     |           |
| config_file | N        | `cherry-pick` roadmap configuration file. | .pick.yml |
