---
name: update-github-info
description: Refreshes the GitHub Info website page with recent GitHub Blog and Changelog highlights and opens a pull request for review.
on:
  schedule: daily
  workflow_dispatch:
permissions:
  contents: read
  copilot-requests: write
engine:
  id: copilot
  copilot-sdk: true
network:
  allowed:
    - defaults
    - github.blog
    - github.com
tools:
  edit:
  web-fetch:
safe-outputs:
  create-pull-request:
    title-prefix: "[github-info] "
    labels: [website, automation]
    draft: false
    allowed-files:
      - site/content/github-info.md
---

# Update GitHub Info

You maintain the GitHub Info website page for Mona. Refresh it with recent,
practical GitHub updates and propose the change as a pull request. Never write
directly to the default branch.

## Steps

1. Read `notes/mona-notes.md` and follow its editorial guidance: keep summaries
   short and practical, prefer updates that help developers learn GitHub faster,
   and mention the source for every GitHub Blog or Changelog item.
2. Use web fetch to read the latest GitHub Blog posts at
   `https://github.blog/latest/`.
3. Use web fetch to read the latest GitHub Changelog entries at
   `https://github.blog/changelog/`.
4. Read the current `site/content/github-info.md`. Update it by adding or
   refreshing the "Recent GitHub Blog and Changelog stories worth watching"
   theme and any other sections that the new information affects. Keep the
   existing structure and the Mona editorial angle. Do not invent facts; only
   include items you actually read in steps 2 and 3, and link each one to its
   source URL.
5. Only modify `site/content/github-info.md`. If nothing new and relevant is
   found, make no changes and do not create a pull request.
6. When you change the page, the safe output pull request is created
   automatically. In the pull request description, summarize what changed and
   list the sources used, so Mona can review it before it goes live.
