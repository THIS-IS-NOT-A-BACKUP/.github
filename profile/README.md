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
  # Optional, defaults to main
  UPSTREAM_BRANCH: "main"
  # Optional, defaults to UPSTREAM_BRANCH
  DOWNSTREAM_BRANCH: ""
  # Optional fetch arguments
  FETCH_ARGS: ""
  # Optional merge arguments
  MERGE_ARGS: ""
  # Optional push arguments
  PUSH_ARGS: ""
  # Optional toggle to spawn time logs (keeps action active) 
  SPAWN_LOGS: "false" # "true" or "false"

# This runs every day on 1801 UTC
on:
  schedule:
    - cron: '1 18 * * *'
  # Allows manual workflow run (must in default branch to work)
  workflow_dispatch:

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: GitHub Sync to Upstream Repository
        uses: dabreadman/sync-upstream-repo@v1.3.0
        with: 
          upstream_repo: ${{ env.UPSTREAM_URL }}
          upstream_branch: ${{ env.UPSTREAM_BRANCH }}
          downstream_branch: ${{ env.DOWNSTREAM_BRANCH }}
          token: ${{ env.WORKFLOW_TOKEN }}
          fetch_args: ${{ env.FETCH_ARGS }}
          merge_args: ${{ env.MERGE_ARGS }}
          push_args: ${{ env.PUSH_ARGS }}
          spawn_logs: ${{ env.SPAWN_LOGS }}
```
<!--

**Here are some ideas to get you started:**

🙋‍♀️ A short introduction - what is your organization all about?
🌈 Contribution guidelines - how can the community get involved?
👩‍💻 Useful resources - where can the community find your docs? Is there anything else the community should know?
🍿 Fun facts - what does your team eat for breakfast?
🧙 Remember, you can do mighty things with the power of [Markdown](https://guides.github.com/features/mastering-markdown/)
-->
