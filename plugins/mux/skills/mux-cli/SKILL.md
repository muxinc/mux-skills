---
name: mux-robots
description: Use when running AI workflows on Mux video with Mux Robots — summarizing videos, generating titles/descriptions/tags/chapters, content moderation, asking questions about a video, finding key moments or scenes, translating or editing captions, picking best thumbnails, or engagement insights. Triggers on "Mux Robots", robots directives, or `mux robots` CLI commands.
---

# Mux Robots

Mux Robots run AI-powered workflows on video assets: you point a robot at an asset ID, it runs as an asynchronous job, and you collect the result. The `mux` CLI is the fastest way to run them.

## Workflow

1. Start a job against an asset (examples):

   ```bash
   mux robots summarize <asset-id> --agent
   mux robots generate-chapters <asset-id> --agent
   mux robots moderate <asset-id> --agent
   mux robots ask-questions <asset-id> --agent
   mux robots find-key-moments <asset-id> --agent
   mux robots translate-captions <asset-id> --agent
   ```

2. Jobs are asynchronous. Track them:

   ```bash
   mux robots list --agent          # all jobs
   mux robots get <job-id> --agent  # status + results
   mux robots cancel <job-id> --agent
   ```

Each robot has its own flags (e.g. `summarize` takes `--description-length`, `--tag-count`). Run `mux robots <robot> --help` for the exact options — do not guess flag names.

## Available robots

| Robot | What it produces |
| --- | --- |
| `summarize` | Title, description, and tags for a video |
| `generate-chapters` | Chapter markers with titles |
| `moderate` | Content moderation signals |
| `ask-questions` | Answers to natural-language questions about the video |
| `find-key-moments` | Timestamps of notable moments (pairs well with clipping — see the `mux-clipping` skill) |
| `translate-captions` | Captions translated to another language |

The robot catalog grows over time (find-scenes, best thumbnails, premium captions, audio translation, engagement insights are documented). If a robot exists in the docs but not in the installed CLI, use the REST API per the docs, or suggest upgrading the CLI.

## Conventions and pitfalls

- **The asset must be ready.** Robots run on processed assets — wait for `video.asset.ready` before starting a job.
- **Jobs are asynchronous.** Don't block on results synchronously in an app; store the job ID and check status, or handle the completion webhook if the app uses webhooks.
- Robots operate on **asset IDs**, not playback IDs.
- Results may need human review before publishing (especially `moderate` and generated metadata) — surface them as suggestions in UIs, not silent writes.
- **Robots directives** let you steer robot behavior (tone, format, constraints) — fetch the directives doc before hand-rolling prompt-like options.

## Docs

| Topic | URL |
| --- | --- |
| Robots overview | https://www.mux.com/docs/guides/robots.md |
| Robots directives | https://www.mux.com/docs/guides/robots-directives.md |
| Summarize | https://www.mux.com/docs/guides/robots-summarize.md |
| Moderate | https://www.mux.com/docs/guides/robots-moderate.md |
| Generate chapters | https://www.mux.com/docs/guides/robots-generate-chapters.md |
| Ask questions | https://www.mux.com/docs/guides/robots-ask-questions.md |
| Find key moments | https://www.mux.com/docs/guides/robots-find-key-moments.md |
| Translate captions | https://www.mux.com/docs/guides/robots-translate-captions.md |
| Find scenes | https://www.mux.com/docs/guides/robots-find-scenes.md |
| Best thumbnails | https://www.mux.com/docs/guides/robots-find-best-thumbnails.md |

If a URL 404s, search https://www.mux.com/llms.txt for the current location.
