---
name: mux-docs
description: Use for any question about Mux APIs, SDKs, the mux CLI, webhooks, assets, uploads, playback, live streaming, Mux Data, or Mux Robots. Finds the current Mux documentation — Mux publishes every docs page as LLM-ready markdown indexed at mux.com/llms.txt — so answers come from today's published docs instead of web search or model memory.
---

# Mux docs discovery

Mux publishes its entire documentation as agent-ready markdown, auto-generated from the same source as the real docs site. For any Mux question, fetch the relevant page and answer from it — never answer Mux API questions from memory, because API shapes and guidance change.

## Workflow

1. **Route.** Pick the most specific starting point:
   - A known page URL (see collection indexes below to find one).
   - A collection index for the topic area (small, fast to scan).
   - https://www.mux.com/llms.txt — the master index of every docs page — when you don't know where the topic lives.
2. **Fetch** the page's markdown. Every docs page has a markdown version: append `.md` to its URL (e.g. `https://www.mux.com/docs/guides/start-live-streaming.md`).
3. **Answer from the fetched content** and cite the page URL.

## Collection indexes

| Collection | URL |
| --- | --- |
| Core concepts | https://www.mux.com/docs/core.txt |
| Video: upload, encode, manage assets | https://www.mux.com/docs/guides/video.txt |
| Uploader: handle user uploads | https://www.mux.com/docs/guides/uploader.txt |
| Player: embed video playback | https://www.mux.com/docs/guides/player.txt |
| Data: playback quality and analytics | https://www.mux.com/docs/guides/data.txt |
| Data integrations: third-party player monitoring | https://www.mux.com/docs/guides/data-integrations.txt |
| Framework integrations and SDKs | https://www.mux.com/docs/integrations.txt |
| Example implementations | https://www.mux.com/docs/examples.txt |
| Pricing and billing | https://www.mux.com/docs/pricing.txt |

`https://www.mux.com/llms-full.txt` is the entire documentation in one file — very large; prefer per-page fetches.

## Self-healing

If a docs URL 404s, the docs have likely been reorganized. Do not give up after one 404: fetch https://www.mux.com/llms.txt, search it for the topic, and use the current URL.

## Staying in sync

- This skill is distributed from the `muxinc/skills` repository. If the Mux CLI is installed, refresh installed skills with `mux skills update`; otherwise pull the latest from https://github.com/muxinc/skills.
- If the installed `mux` CLI provides `mux docs` subcommands (`mux docs search` / `mux docs read` — available in newer versions), prefer them over raw fetching: they search a downloaded copy of the same published docs. Check with `mux docs --help`; if the command doesn't exist, use the fetch workflow above.

## Guardrails

- Cite the docs page URL you answered from.
- If the network is unavailable, say you could not verify against current docs — never guess API request/response shapes from memory.
