# Mux Agent Skills

Skills that teach AI coding agents how to build with [Mux](https://mux.com) — the CLI, the API, and current documentation — so agents build with Mux correctly on the first try.

This repo is the source of truth for all Mux agent skills and doubles as the Claude Code plugin marketplace. Skills follow the cross-agent [Agent Skills](https://agentskills.io) standard (`SKILL.md`), so they work in Claude Code, OpenAI Codex, GitHub Copilot, Cursor, Gemini CLI, VS Code, and any other agent that supports the format.

## Install

### Claude Code (plugin marketplace)

```
/plugin marketplace add muxinc/skills
/plugin install mux@mux
```

### Mux CLI

```bash
mux skills install
```

Writes the skills into detected agent directories (`.claude/skills/`, Codex/Cursor equivalents) at project level by default, with a version stamp so the CLI can offer a refresh on upgrade.

### Manual

Copy `plugins/mux/skills/*` into your agent's skills directory (e.g. `.claude/skills/`).

## Skills

| Skill | What it does |
| --- | --- |
| [`mux`](plugins/mux/skills/mux/SKILL.md) | General Mux skill: CLI auth and command map, webhooks-for-local-dev flow, docs routing to live markdown docs, and conventions/pitfalls (don't poll asset status, verify webhook signatures, playback ID vs. asset ID, signed vs. public policy). |
| [`mux-docs`](plugins/mux/skills/mux-docs/SKILL.md) | Docs discovery via the Mux CLI: `mux docs search` / `mux docs read` before web search or memory, and `mux docs update` to keep the local docs index current. |
| [`mux-clipping`](plugins/mux/skills/mux-clipping/SKILL.md) | Clipping workflows: choosing between instant clips (playback URL parameters, no re-encoding) and asset-based clips (`mux://assets` input with `start_time`/`end_time`), with the pitfalls of each. |
| [`mux-robots`](plugins/mux/skills/mux-robots/SKILL.md) | AI workflows on video with Mux Robots: summarize, chapters, moderation, key moments, caption translation via `mux robots`, plus async job handling and directives. |

## Design principles

**Skills point at live docs; they don't copy them.** A doc snapshot is stale the day after release. Mux publishes LLM-ready docs — `https://www.mux.com/llms.txt` indexes 200+ per-page markdown files — auto-generated from the same source as the real docs. The skills carry only what a network fetch cannot provide:

1. **Routing** — a curated task-to-URL map so agents fetch the right doc instead of reasoning over the full index every session.
2. **CLI knowledge** — commands, flags, auth, env vars, the `--agent` flag. Not on docs.mux.com and versioned with the CLI.
3. **Procedure and pitfalls** — the support-engineer knowledge layer.

Anything that changes with the Mux API lives on the network; anything that routes, is CLI-specific, or is judgment lives in the skill.

## Repository structure

```
.
├── .claude-plugin/marketplace.json   # Claude Code plugin marketplace manifest
└── plugins/mux/
    ├── .claude-plugin/plugin.json    # plugin manifest
    └── skills/
        ├── mux/
        │   ├── SKILL.md
        │   └── references/doc-index.md
        ├── mux-docs/SKILL.md
        ├── mux-clipping/SKILL.md
        └── mux-robots/SKILL.md
```

## Contributing

- Keep skills tightly scoped and procedural — no doc dumps.
- The CLI command map in `plugins/mux/skills/mux/SKILL.md` must match the released `muxinc/cli`. If you change CLI commands, update the skill in the same release cycle (this is on the CLI release checklist).
- If a docs URL goes stale after a docs reorg, fix the route in `references/doc-index.md`.

## License

MIT
