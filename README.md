# Mux Agent Skills

Skills that teach AI coding agents how to build with [Mux](https://mux.com) — the CLI, the API, and current documentation.

### Install

Clone this repo and copy `plugins/mux/skills/*` into your agent's skills directory (e.g. `.claude/skills/`). Skills are plain `SKILL.md` files with no dependency on the Mux CLI — they work in any agent that supports the [Agent Skills](https://agentskills.io) format.

## Skills

| Skill | What it does |
| --- | --- |
| [`mux-docs`](plugins/mux/skills/mux-docs/SKILL.md) | Docs discovery: routes agents to Mux's live LLM-ready docs (`mux.com/llms.txt`, collection indexes, per-page markdown) so answers come from today's published docs, not web search or model memory. |
# mux-skills
