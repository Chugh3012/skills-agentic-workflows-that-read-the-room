---
name: update-github-info

"on":
  schedule: daily
  workflow_dispatch:

permissions:
  contents: read
  pull-requests: read

tools:
  edit:
  web-fetch:

network:
  allowed:
    - github.blog
    - github.com
    - awesome-copilot.github.com

safe-outputs:
  create-pull-request:
    title-prefix: "[github-info] "
    draft: true
    max: 1
    allowed-files:
      - site/content/github-info.md
---

# Update GitHub Info

Keep `site/content/github-info.md` current with practical, developer-focused information from official GitHub sources.

1. Read `notes/mona-notes.md` for Mona's editorial guidance.
2. Read the current `site/content/github-info.md` before making changes.
3. Use the `web-fetch` tool to fetch `https://github.blog/latest/`.
4. Use the `web-fetch` tool to fetch `https://github.blog/changelog/`.
5. Use the `web-fetch` tool to fetch `https://awesome-copilot.github.com/workflows/` and include relevant Awesome Copilot workflows among the sources.
6. Update only `site/content/github-info.md` with concise, useful changes supported by those sources. Preserve accurate existing content, avoid speculation, and link each new item to its source.
7. If there are no meaningful updates, do not change the file and do not open a pull request.
8. If the file changed, use the `create_pull_request` safe-output tool exactly once to open a draft pull request for Mona to review. Use a descriptive branch name, summarize the sources and changes in the pull request body, and do not push directly to `main`.