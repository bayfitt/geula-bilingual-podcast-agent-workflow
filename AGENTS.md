# Coordinator contract

## Mission

Produce a source-grounded Hebrew master and aligned English edition for each eligible new item in the configured feed queue. The Hebrew master is authoritative. The work is complete only when the required content, source, audio, artwork, and publication checks pass and the live records are read back.

## Run rules

1. Read the private project configuration, both source ledgers, and the current in-progress episode before selecting work. Reconcile the article and video queues by canonical URL or stable video ID. Resume the oldest unresolved `in_progress` item. Do not skip it to start newer work.
2. If no eligible new item exists, make no changes and remain quiet. Skip items already `published_bilingual`. Resume an existing item in its dated folder; do not duplicate or overwrite completed artifacts.
3. Select eligible items by source publication time, oldest first. Do not backfill pre-baseline material unless directly requested.
4. Use the agent briefs in `agents/`. Keep responsibilities bounded. A source researcher does not write the script; a translator does not alter the Hebrew master; an auditor does not rewrite prose; a publisher does not certify source truth.
5. Perform one atomic action at a time. Save that action's direct evidence, then ask Jev one narrow question per independent criterion. Continue only when each required result is `yes=true` at confidence **0.95 or higher**. Never batch unrelated actions or criteria.
6. Preserve every failure, retry, correction, model/provider name, token count, and provider-displayed approximate cost in the private episode audit. Mark estimates as estimates; do not present them as billed cost.
7. Jev is a consistency check only. Verify source texts directly. Verify actual file hashes, model/voice/settings, playback, rendered artwork, caption format if enabled, and live service state independently.
8. If a source, credential, local machine, browser, or authenticated service is unavailable, stop at that exact gate. Do not bypass authentication, silently substitute a provider, or claim success.
9. Keep captions paused unless the user explicitly resumes them. While paused, do not generate, time, validate, upload, or attach SRT/VTT files; caption absence is not a release gate.
10. Publish only if the active project configuration records user authorization for automatic publication and every release gate passes. Otherwise prepare a reviewable draft and wait for the authorized next step.
11. Update a ledger to `published_bilingual` only after both language episodes are present in the public service, their live records and playback are verified, and the episode URLs are recorded. A local export or “published” wizard state is not sufficient.
12. Keep this repository clean. All episode-specific files and evidence stay in the private workspace; never copy credentials, voice IDs, raw article text, personal data, ledgers, source captures, or media into this repo.

## Required agent order

`source-discovery → source-research → linear-sugya-editor → Hebrew-master-writer → Luna-Max-translator → Hebrew-origin-auditor → metadata-editor → audio-producer → caption-producer (only if resumed) → artwork-agent → publisher → audit-archivist`

Run these sequentially where outputs depend on one another. Do not parallelize state-changing work. Read-only retrieval can be parallelized only when the run's atomic evidence rules allow it and each result is checked before dependent work begins.

## Stop conditions

- No canonical source identity, conflicting queue state, or an older unresolved queue item.
- A required Jev answer is false, missing, or below 0.95 after the correction attempt.
- A primary source cannot be located or a material claim cannot be supported, qualified, or omitted without distorting the article.
- Hebrew and English do not cover the same ordered claims, names, citations, or limitations.
- Actual audio differs from the approved transcript, voice/model changes unexpectedly, or the assembled file fails integrity checks.
- A caption pause is active and a proposed action would create or upload caption files.
- Artwork text, language, crop, or mobile-size legibility is uncertain.
- Creator access, public page, live metadata, playback, or service readback is unavailable or ambiguous.

At a stop, preserve artifacts and the exact failed criterion, keep the item `in_progress`, report the blocker, and do not claim publication.
