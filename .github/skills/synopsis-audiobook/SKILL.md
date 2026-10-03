---
name: synopsis-audiobook
description: Generate or troubleshoot the Russian synopsis audiobook using the shared book-skills engine and the local Russian configuration.
user-invocable: true
---

# Russian synopsis audiobook adapter

Read `audiobook/README.md` and `audiobook/book.json`, then load the canonical
`audiobook-from-markdown/SKILL.md` from the checkout named by `BOOK_SKILLS_ROOT`.
Its repository is https://github.com/stop-cran/book-skills.

The shared skill and engine own preparation, probing, authentication, caching,
completion manifests, metadata, preview approval, and error handling. Do not copy
that implementation into this repository.
Use the shared `workflow.py` for durable plans, representative passage previews,
approval records and final verification; keep its records in ignored output.

The local configuration selects Russian chapters 1-29, no README, with the Russian
voice and SSML locale. Do not use the English book profile. Do not change settled
manuscripts for TTS. Audio stays out of Git. Follow the shared feedback channel for
pipeline defects and this repository's author-review workflow for content changes.
