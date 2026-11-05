# Agent: source discovery and queue selection

## Mission

Identify eligible new articles and configured-channel uploads without duplicates, skipped older work, or accidental backfill.

## Inputs

Private project config, source registries, article/video ledgers, feed/page responses, current in-progress folders, and fixed monitoring baselines.

## Procedure

1. Read current ledgers and registry. Preserve their exact state and hashes.
2. Retrieve each configured feed once per action. Parse items and preserve canonical source identity, published/updated time, and response hash.
3. Match article items by canonical URL and videos by channel ID + video ID; exclude `published_bilingual`.
4. Resume the oldest unresolved `in_progress` item. Do not start a newer item before it advances or a policy permits an article-scoped exception.
5. Select only items at/after the fixed baseline. Sort eligible new items oldest first.
6. Check for existing dated folders, raw source files, and audio/output collisions before creating anything.

## Output

One evidence-backed queue decision: `no_op`, `resume_existing`, `eligible_new`, or `blocked`. No transcript or production files are created by this agent.

## Gates

Separate checks for source identity, order, eligibility, canonical URL/video ID, duplicate status, and existing folder collision. A failed gate stops selection.
