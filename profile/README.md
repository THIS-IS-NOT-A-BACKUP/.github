## Hi there 👋. This organisation is created to mirror open-sourced tools, and maintain the histories in case where projects were made unavailable.

Sync with this template below, replace any fields in `env` to your use cases.

```yaml
# Template to sync with upstream
name: Sync Upstream

env:
  # Required, URL to upstream (fork base)
  UPSTREAM_URL: "https://github.com/<usr>/<repo>.git"
  # Required, token to authenticate bot, could use ${{ secrets.GITHUB_TOKEN }} 
  # Over here, we use a PAT instead to authenticate workflow file changes.
  WORKFLOW_TOKEN: ${{ secrets.WORKFLOW_TOKEN }}
  # Required, is usually "master" or "main"
  UPSTREAM_BRANCH: "master"
  # Optional, defaults to UPSTREAM_BRANCH
  DOWNSTREAM_BRANCH: ""
  # Optional merge arguments
  MERGE_ARGS: ""
  # Optional push arguments
  PUSH_ARGS: ""

# This runs every day on 1801 UTC
on:
  # Or on push, if for mirror it runs on workflow setup and changes
  # push:
  schedule:
    - cron: '1 18 * * *'
  # Allows manual workflow run (must in default branch to work)
  workflow_dispatch:

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: GitHub Sync to Upstream Repository
        uses: dabreadman/sync-upstream-repo@v1.2.0.b
        # use v1.1.0.b if you do not want to spawn persistent log file
        # that is to prevent action from disabling after 6 months
        with: 
          upstream_repo: ${{ env.UPSTREAM_URL }}
          upstream_branch: ${{ env.UPSTREAM_BRANCH }}
          downstream_branch: ${{ env.DOWNSTREAM_BRANCH }}
          token: ${{ env.WORKFLOW_TOKEN }}
          merge_args: ${{ env.MERGE_ARGS }}
          push_args: ${{ env.PUSH_ARGS }}

```
<!--

**Here are some ideas to get you started:**

🙋‍♀️ A short introduction - what is your organization all about?
🌈 Contribution guidelines - how can the community get involved?
👩‍💻 Useful resources - where can the community find your docs? Is there anything else the community should know?
🍿 Fun facts - what does your team eat for breakfast?
🧙 Remember, you can do mighty things with the power of [Markdown](https://guides.github.com/features/mastering-markdown/)
-->
