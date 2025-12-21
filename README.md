# Notes & Takeaways

This repo is a content pipeline:

- material/<topic>/ : raw notes, errors, commands, and context (raw truth)
- result/<topic>/   : publishable outputs
  - article.md  (<= 6 min read)
  - threads.md  (short summary for Threads)

## Rules

- Hard rules (non-negotiable): .specify/memory/constitution.md
- Soft rules + output contract: .specify/memory/spec.md

Important:
- Never generate outputs on the `master` branch.
- Each generation must only touch a single topic:
  material/<topic>/ -> result/<topic>/

## Create a new post (topic)

1) Create a branch:
- git checkout -b post/<topic>

2) Create folders:
- material/<topic>/
- result/<topic>/
- specs/<topic>/ (optional)

3) Write raw notes:
- material/<topic>/draft.md (required)
- snippets.md / context.md / links.md (optional)

4) Generate drafts (Copilot Chat / prompt files):
- /gen-article topic=<topic>
- /gen-short topic=<topic>

If your environment doesn't support `topic=<topic>` arguments:
- run /gen-article then add: topic: <topic>
- run /gen-short then add: topic: <topic>

5) Edit only:
- result/<topic>/article.md
- result/<topic>/threads.md

6) Commit + PR merge back to master.