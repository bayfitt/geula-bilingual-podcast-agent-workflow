# Atomic gates and evidence contract

## Gate threshold

The example project uses Jev threshold **0.95**. One independent criterion gets one short, narrow Jev question. If an action has four independent acceptance criteria, make four calls. Do not bundle source accuracy, translation quality, citation form, and disclosure presence into one confidence score.

Continue only on `yes=true` and confidence ≥ 0.95. Preserve `false`, missing scores, API errors, and low-confidence results. A narrower retry is allowed only after a concrete evidence or wording correction; keep the previous result and label the retry. If a required criterion remains unresolved, stop its dependent stages. Do not treat Jev as source authority.

## Atomic action IDs

Use monotonically numbered IDs per episode, such as `SRC-0001`, `CLAIM-0004`, `MAP-0002`, `HE-0012`, `EN-0012`, `AUDIT-0012`, `TTS-EN-0003`, `ART-HE-0001`, `SPOTIFY-EN-0002`, `READBACK-HE-0007`, and `LEDGER-0003`.

An atomic action is one feed fetch, source retrieval, claim extraction, source mapping, outline move, paragraph draft or translation, correction, tool/API call, file write, audio chunk, caption response, artwork operation, Spotify mutation, or service readback. Do not combine multiple writes or uploads under one ID. For each action: perform it, save direct evidence and hash, ask Jev immediately, append the result, and only then consider the next action.

## JSONL audit fields

Each Jev call is one JSON object with at least:

```json
{
  "action_id": "EN-0012",
  "timestamp_utc": "2026-01-01T00:00:00Z",
  "question": "Does paragraph 12 preserve the Hebrew master's conditional wording?",
  "evidence_path": "evidence/EN-0012.txt",
  "evidence_sha256": "<sha256>",
  "provider": "<provider>",
  "model": "<model>",
  "yes": true,
  "confidence": 0.97,
  "input_tokens": 410,
  "output_tokens": 20,
  "provider_displayed_approximate_cost_usd": 0.00002,
  "cost_is_estimate": true,
  "error": null
}
```

Use `null` for values not returned. Never invent tokens, usage, or costs. Clearly label rate-derived values as estimates and say when exact credits/billed cost are unavailable. Append rather than rewrite; corrections get new IDs.

## Evidence quality

- Prefer compact, criterion-specific excerpts over whole feeds or whole episodes.
- Store original provider/API responses separately from normalized text.
- Preserve URL, retrieval timestamp, model/provider, request settings, and content hash.
- Do not put secrets, cookies, auth headers, or unrestricted personal data in evidence.
- A source map can point to an exact source excerpt but cannot replace directly opening and verifying that source.
- A Jev pass confirms consistency with submitted evidence only; it does not establish that the source itself is true or authoritative.

## End-of-run accounting

Calculate totals from the append-only audit after all checks. Report call count, pass/fail/error counts, confidence range, input/output tokens, and sum of provider-displayed approximate costs. Keep global and per-episode logs clearly distinguished if one duplicates the other. Never call an estimate an invoice amount.
