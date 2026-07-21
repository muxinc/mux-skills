---
name: mux-docs
description: Use for any question about Mux APIs, SDKs, the mux CLI, webhooks, assets, uploads, playback, live streaming, Mux Data, or Mux Robots when the mux CLI is installed. Fetches the latest published Mux documentation with `mux docs update` and searches it with `mux docs search` / `mux docs read` — always prefer this over web search or answering from memory.
---

# Mux docs discovery

The `mux` CLI does not ship with documentation. That is the point: `mux docs update` downloads the latest published docs from docs.mux.com, and `mux docs search` / `mux docs read` query that download — so answers always reflect what Mux publishes today, not whatever the CLI or the model was trained on. For any Mux question, use this before web search or answering from memory.

## Workflow

1. Fetch the latest published docs (also run this whenever the download might be old — it is a snapshot from the moment it was fetched):

   ```bash
   mux docs update
   ```

2. Search the docs:

   ```bash
   mux docs search "<topic>" --json
   ```

3. Read the most relevant result:

   ```bash
   mux docs read "<doc-id>" --format markdown
   ```

4. Answer using the retrieved content. Cite the page by its `doc.id` and `doc.url`.

Only fall back to web search if the search fails, the docs have no relevant result, or the user explicitly asks for external results. If nothing matches, the network fallback is https://www.mux.com/llms.txt (index of every docs page as markdown).

## Keeping docs up to date

What `mux docs update` downloads is the docs published at that moment (manifest and index from `docs.mux.com/.well-known/mux-docs/`). Re-run it:

- Before answering, if you have not updated in this session.
- Whenever `mux docs search` reports a missing or empty download.
- If results look stale — a doc contradicts observed API behavior, or the user says the docs changed.

For local pre-deploy testing against generated artifacts in a `mux.com` checkout:

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
