---
name: update-github-info
description: Keep the GitHub Info page current with concise, practical updates from official GitHub Blog and Changelog posts.
intent: Help Mona keep the GitHub Info page useful and current with concise, source-linked guidance for developers.
model: gpt-4.1
on:
  schedule: daily
  workflow_dispatch:
permissions:
  contents: read
tools:
  bash: [cat]
  edit: true
  web-fetch: {}
network:
  allowed:
    - defaults
    - github.blog
    - github.com
    - awesome-copilot.github.com
safe-outputs:
  create-pull-request:
    max: 1
    draft: false
    allowed-files:
      - site/content/github-info.md
---

Read `notes/mona-notes.md` and the current `site/content/github-info.md` before making changes.

Use the web-fetch tool to read all three:

- https://github.blog/latest/
- https://github.blog/changelog/
- https://awesome-copilot.github.com/workflows/

Select only timely, useful items that fit Mona's editorial guidance and help developers learn GitHub. Keep updates short and practical, preserve the page's existing structure, and link to the official source for every update. Do not invent details or add items that are not supported by the fetched sources.

Edit only `site/content/github-info.md`. If there is no relevant, well-supported update, make no changes and call `noop` rather than opening an empty pull request.

When the page has a meaningful update, use the create-pull-request safe output to open one non-draft pull request with a concise title and a body that summarizes the changes, cites the source links, and presents the updates for Mona to review. Do not merge the pull request.
