# GitHub Activity in Readme

The purpose of this action is to update the `README.md` file with the recent GitHub activity of a user.

<img width="735" alt="profile-repo" src="https://github.com/manueldevjour/github-activity-readme/blob/master/assets/general.jpeg">

## Instructions

1. Add the comment `<!--START_SECTION:activity-->` (entry point) within `README.md`. You can find an example [here]()

2. Now you have to create a workflow file.

`.github/workflows/update-readme.yml`

```yml
name: Update README

on:
  schedule:
    - cron: '*/30 * * * *'
  workflow_dispatch:

jobs:
  build:
    runs-on: ubuntu-latest
    name: Update this repo's README with recent activity

    steps:
      - uses: actions/checkout@v2
      - uses: manueldevjour/github-activity-readme@master
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

3. Create a GitHub token. You have to create a [personal access token](https://github.com/settings/tokens?type=beta). You can find more information [here](https://help.github.com/en/github/authenticating-to-github/creating-a-personal-access-token-for-the-command-line). I gave permissions on everything until I test it more. You can give less permissions if you want.

<img width="735" alt="profile-repo" src="https://github.com/manueldevjour/github-activity-readme/blob/master/assets/create-token.jpeg">

4. Go to your repository > Settings > Secrets and variables > Actions > New repository secret  Secret part of repository for using it and call it as `GH_TOKEN` and paste your token in the value part.

<img width="735" alt="profile-repo" src="https://github.com/manueldevjour/github-activity-readme/blob/master/assets/token-secret.jpeg">


The above job runs every half an hour, you can change it as you wish based on the [cron syntax](https://jasonet.co/posts/scheduled-actions/#the-cron-syntax).


### Override defaults

Use the following `input params` to customize it for your use case:-

| Input Param | Default Value | Description |
|--------|--------|--------|
| `COMMIT_MSG` | :zap: Update README with the recent activity | Commit message used while committing to the repo |
| `MAX_LINES` | 5 | The maximum number of lines populated in your readme file |


```yml
name: Update README

on:
  schedule:
    - cron: '*/30 * * * *'
  workflow_dispatch:

jobs:
  build:
    runs-on: ubuntu-latest
    name: Update this repo's README with recent activity

    steps:
      - uses: actions/checkout@v2
      - uses: jamesgeorge007/github-activity-readme@master
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
        with:
          COMMIT_MSG: 'Specify a custom commit message'
          MAX_LINES: 10
```

---------------------------------------

_Inspired by [JasonEtco/activity-box](https://github.com/JasonEtco/activity-box) and [jamesgeorge007/github-activity-readme](https://github.com/jamesgeorge007/github-activity-readme)_

