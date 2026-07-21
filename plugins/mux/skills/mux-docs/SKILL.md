---
name: mux-docs
description: Use for any question about Mux APIs, SDKs, the mux CLI, webhooks, assets, uploads, playback, live streaming, Mux Data, or Mux Robots when the mux CLI is installed. Discovers current Mux documentation locally with `mux docs search` and `mux docs read`, and keeps the local docs cache up to date with `mux docs update` — always prefer this over web search or answering from memory.
---

# Mux docs discovery

The `mux` CLI ships a local, searchable index of the current Mux documentation. For any Mux question, search this index before using web search or answering from memory — API shapes and guidance change, and the local index matches what Mux publishes today.

## Workflow

1. Search the docs index:

   ```bash
   mux docs search "<topic>" --json
   ```

2. Read the most relevant result:

   ```bash
   mux docs read "<doc-id>" --format markdown
   ```

3. Answer using the retrieved content. Cite the page by its `doc.id` and `doc.url`.

Only fall back to web search if the search fails, the index has no relevant result, or the user explicitly asks for external results. If the index has nothing, the network fallback is https://www.mux.com/llms.txt (index of every docs page as markdown).

## Keeping docs up to date

The index is a local cache. Keep it current:

- If `mux docs search` reports an empty or missing cache, populate it:

  ```bash
  mux docs update
  ```

- If results look stale (a doc contradicts observed API behavior, or the user says the docs changed), run `mux docs update` and search again.
- For local pre-deploy testing against generated artifacts in a `mux.com` checkout:

  ```bash
  mux docs update --artifact-path ../mux.com/apps/web/public/.well-known/mux-docs
  ```

### Docs sources

The CLI resolves docs in this order:

1. Cached published manifest/index populated by `mux docs update` (downloaded from docs.mux.com)
2. `--source <path>`
3. `MUX_DOCS_PATH`
4. A sibling `../mux.com` checkout, for local Mux development

## Inside the CLI repo

If working in the `muxinc/cli` repo itself and `mux` is not installed globally, use the dev entrypoint:

```bash
pnpm dev docs search "<topic>" --json
pnpm dev docs read "<doc-id>" --format markdown
```

## Example

User asks: "How do I verify Mux webhook signatures?"

```bash
mux docs search "verify webhook signatures" --json
mux docs read verify-webhook-signatures --format markdown
```

Then answer from the retrieved doc, citing its `doc.id` and `doc.url`.

## Guardrails

- Do not mutate Mux resources (create/update/delete) unless the user explicitly asks.
- For write or delete operations, state the intended action first and confirm if there is any ambiguity — deletes are permanent.
