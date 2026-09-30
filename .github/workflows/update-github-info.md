---
name: update-github-info
description: Keep Mona's GitHub Info page current with practical updates from the official GitHub Blog and Changelog.
on:
  schedule: daily
  workflow_dispatch:
permissions:
  contents: read
engine: copilot
tools:
  edit:
  web-fetch:
network:
  allowed:
    - github.blog
    - github.com
safe-outputs:
  create-pull-request:
    max: 1
    draft: false
---

# Update GitHub Info

Refresh `site/content/github-info.md` with concise, useful GitHub updates for Mona's website. Propose all changes in one pull request for Mona to review; never write or push changes directly to `main`.

## Sources and context

1. Read `notes/mona-notes.md` and the current `site/content/github-info.md` before making changes.
2. Use the `web-fetch` tool to fetch both official sources:
   - https://github.blog/latest/
   - https://github.blog/changelog/
3. Base updates only on information confirmed by those pages and the linked official posts. Do not infer details or use unverified claims.

## Editorial rules

- Keep summaries short, practical, and useful to developers learning GitHub.
- Preserve the existing editorial angle, useful content, and overall structure of `site/content/github-info.md`.
- Update only `site/content/github-info.md`; do not modify any other file.
- Add or refresh a concise recent-updates section with no more than three timely, relevant items. Include each item's title, a brief practical summary, and a direct source link identifying whether it came from the GitHub Blog or Changelog.
- Skip stories that do not provide a useful update for the site's audience. If there is no meaningful content change to make, do not open a pull request.

## Pull request

When there is a meaningful content change, inspect the working-tree changes and ensure only `site/content/github-info.md` is included. Create a unique local branch, commit only that file, and do not push. Then call the configured `create_pull_request` safe output exactly once with a clear title and a concise body that asks Mona to review the update and links to the source stories. Stop after submitting the pull request.