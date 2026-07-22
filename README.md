# Mux Agent Skills

Skills that teach AI coding agents how to build with [Mux](https://mux.com) — the CLI, the API, and current documentation.

### Install

Clone this repo and copy `plugins/mux/skills/*` into your agent's skills directory (e.g. `.claude/skills/`). Skills are plain `SKILL.md` files with no dependency on the Mux CLI — they work in any agent that supports the [Agent Skills](https://agentskills.io) format.

## Skills

| Skill | What it does |
| --- | --- |
| [`mux`](plugins/mux/skills/mux/SKILL.md) | General Mux skill: CLI auth and command map, webhooks-for-local-dev flow, docs routing to live markdown docs, and conventions/pitfalls (don't poll asset status, verify webhook signatures, playback ID vs. asset ID, signed vs. public policy). |
| [`mux-docs`](plugins/mux/skills/mux-docs/SKILL.md) | Docs discovery: routes agents to Mux's live LLM-ready docs (`mux.com/llms.txt`, collection indexes, per-page markdown) so answers come from today's published docs, not web search or model memory. |
| [`mux-clipping`](plugins/mux/skills/mux-clipping/SKILL.md) | Clipping workflows: choosing between instant clips (playback URL parameters, no re-encoding) and asset-based clips (`mux://assets` input with `start_time`/`end_time`), with the pitfalls of each. |
| [`mux-cli`](plugins/mux/skills/mux-cli/SKILL.md) | Full `mux` CLI reference: auth and environments, every command group (assets, live, uploads, secure playback, webhooks, Mux Data), and Mux Robots AI jobs (summarize, chapters, moderation, key moments, caption translation) with async job handling and directives. |
# mux-skills
