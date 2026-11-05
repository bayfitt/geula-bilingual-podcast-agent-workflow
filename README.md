# Geula bilingual podcast agent workflow

A source-first production playbook for turning eligible articles or lectures into matched Hebrew and English sugya episodes. It defines the agent roles, sequence, evidence record, quality gates, and publication readback. It is deliberately a documentation-and-template repository: episode content, raw sources, recordings, private ledgers, credentials, and show-specific voice IDs belong in a private production workspace.

## Start here

1. Read [`AGENTS.md`](AGENTS.md) for the coordinator contract.
2. Read [`workflow/PRODUCTION_PLAYBOOK.md`](workflow/PRODUCTION_PLAYBOOK.md) for the end-to-end procedure and source-specific branches.
3. Copy [`config/project.example.yaml`](config/project.example.yaml) into a private project configuration and replace the placeholders. Do not commit real account IDs, credentials, voice IDs, episode data, or private URLs.
4. Check [`workflow/STATE_MACHINE.md`](workflow/STATE_MACHINE.md), [`workflow/GATES_AND_EVIDENCE.md`](workflow/GATES_AND_EVIDENCE.md), and [`workflow/RELEASE_CHECKLIST.md`](workflow/RELEASE_CHECKLIST.md) before a run.
5. Start in the configured private workspace. A scheduled run with no eligible new item is a no-op: no files, account changes, or notification.

## Pipeline

`discover → queue → capture → source-map → linear outline → Hebrew master → Luna Max translation → Hebrew-origin audit → descriptions → audio → captions policy → artwork → publish → live readback → ledger closeout`

Every transition is gated. The default confidence threshold in the example profile is **0.95**. Jev checks consistency; it does not replace direct source verification, visual inspection, or service-side readback. Preserve failures and retries. Never advance a dependent stage while one of its required checks is unresolved.

## Included

- Coordinator instructions in `AGENTS.md`.
- Twelve bounded agent briefs in `agents/`.
- Detailed article/video playbook, state machine, evidence contract, and release checklist in `workflow/`.
- Sanitized example configuration, JSON Schemas, episode manifest, and bilingual description templates.
- Recommended private episode-folder layout and spoken-introduction templates.

## Defaults that protect the production account

- Captions are marked paused in the example project profile. Do not call caption or timestamping APIs, generate or validate SRT/VTT, or attach captions until the user explicitly resumes that stage.
- The example config does not authorize automatic publication. Set the publication mode only from a documented user instruction; publish only after every release gate passes.
- The workflow never stores API keys, raw transcripts, private evidence, episode media, processing ledgers, or voice IDs in this repository.
- The public repo contains no episode-level source text. Cite and link sources from private episode records instead of copying long copyrighted passages.

## Repo status

This repo is a workflow specification, not an executable production service. Provider APIs, local scripts, model names, voices, and public show endpoints must be confirmed in the production environment at run time and recorded in the episode manifest. Never infer a successful tool call or publication from a local file alone.
