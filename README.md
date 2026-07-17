# GitHub Activity in Readme

Updates `README.md` with the recent GitHub activity of a user.

<img width="735" alt="profile-repo" src="https://user-images.githubusercontent.com/25279263/87703301-3aa4a500-c7b8-11ea-8eb6-245121997a7b.png">

## Test

<!--START_SECTION:activity-->
1. 🗣 Commented on [#39](https://github.com/AgnesAI-Labs/AgnesAI-Models/issues/39#issuecomment-4990855423) in [AgnesAI-Labs/AgnesAI-Models](https://github.com/AgnesAI-Labs/AgnesAI-Models)
2. ❗ Opened issue [#14](https://github.com/browser-act/skills/issues/14) in [browser-act/skills](https://github.com/browser-act/skills)
3. 🗣 Commented on [#10500](https://github.com/ruanyf/weekly/issues/10500#issuecomment-4840821271) in [ruanyf/weekly](https://github.com/ruanyf/weekly)
4. 🚀 Published release [v0.4 (2026-06-14) — GitHub Pages 主题与样式优化](https://github.com/yansheng836/bilibili-Fanrenpc/releases/tag/v0.4) in [yansheng836/bilibili-Fanrenpc](https://github.com/yansheng836/bilibili-Fanrenpc)
<!--END_SECTION:activity-->

---

## Instructions

- Add the comment `<!--START_SECTION:activity-->` (entry point) within `README.md`. You can find an example [here](https://github.com/jamesgeorge007/jamesgeorge007/blob/master/README.md).

- It's the time to create a workflow file.

`.github/workflows/update-readme.yml`

```yml
name: Update README
on:
  schedule:
    - cron: "*/30 * * * *"
  workflow_dispatch:
jobs:
  build:
    name: Update this repo's README with recent activity
    runs-on: ubuntu-latest
    permissions:
      contents: write

    steps:
      - uses: actions/checkout@v4
      - uses: jamesgeorge007/github-activity-readme@master
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

The above job runs every half an hour, you can change it as you wish based on the [cron syntax](https://jasonet.co/posts/scheduled-actions/#the-cron-syntax).

Please note that only those public events that belong to the following list show up:-

- `IssueEvent`
- `ReleaseEvent`
- `IssueCommentEvent`
- `PullRequestEvent`

You can find an example [here](https://github.com/jamesgeorge007/jamesgeorge007/blob/master/.github/workflows/update-readme.yml).

### Override defaults

Use the following `input params` to customize it for your use case:-

| Input Param        | Default Value                                                            | Description                                               |
| ------------------ | ------------------------------------------------------------------------ | --------------------------------------------------------- |
| `GH_USERNAME`      | Your GitHub username                                                     | Username for which to generate the activity overview      |
| `COMMIT_NAME`      | github-actions[bot]                                                      | Name of the committer                                     |
| `COMMIT_EMAIL`     | 41898282+github-actions[bot]@users.noreply.github.com                    | Email of the committer                                    |
| `COMMIT_MSG`       | :zap: Update README with the recent activity                             | Commit message used while committing to the repo          |
| `EMPTY_COMMIT_MSG` | :memo: empty commit to keep workflow active after 60 days of no activity | Commit message used when there are no updates             |
| `MAX_LINES`        | 5                                                                        | The maximum number of lines populated in your readme file |
| `TARGET_FILE`      | README.md                                                                | The file to insert recent activity into                   |

```yml
name: Update README
on:
  schedule:
    - cron: "*/30 * * * *"
  workflow_dispatch:
jobs:
  build:
    name: Update this repo's README with recent activity
    runs-on: ubuntu-latest
    permissions:
      contents: write

    steps:
      - uses: actions/checkout@v4
      - uses: jamesgeorge007/github-activity-readme@master
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
        with:
          COMMIT_MSG: "Specify a custom commit message"
          MAX_LINES: 10
          COMMIT_NAME: GitHub Activity Readme
```

_Inspired by [JasonEtco/activity-box](https://github.com/JasonEtco/activity-box)_
