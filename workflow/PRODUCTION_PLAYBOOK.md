# End-to-end production playbook

This playbook is the operational source of truth for one article or video. Each numbered phase is made of smaller atomic actions; a phase heading never authorizes batching. Preserve a dated episode folder and an append-only Jev audit for every selected item.

## 0. Preflight and queue reconciliation

Read the private configuration, the article ledger, the video ledger, the source registry, and the existing in-progress episode folder. Confirm the caption setting and publication authorization. Make a single combined queue view keyed by canonical article URL or video ID, but preserve each source ledger as authoritative. Exclude completed `published_bilingual` items, resume existing work at its first unresolved gate, and block newer work behind the oldest unresolved in-progress item. For a fresh item, require its publication time to meet the fixed monitoring baseline. Do not move the baseline to hide pending work.

For each read or comparison: capture the exact file/API response, hash the evidence, record the intended conclusion, and Jev-check that single conclusion. If no eligible source remains, finish as a quiet no-op with no file write, notification, or account change.

## 1. Discover and select a source

### Article path

Fetch the configured RSS feed directly. Save the HTTP status, retrieval time, response hash, and the selected item's title, author, publication timestamp, canonical URL, and item index. Parse the feed locally; do not mistake a feed wrapper, comments page, or title match for the canonical article. If the HTTP client rejects an XML content type, use a direct HTTP client and a local XML parser rather than treating a browser search result as the feed.

### Video path

Read the configured channel registry and identify uploads by channel ID and video ID. Record the title, canonical URL, upload time, newest-item ordering, and available transcript tracks. Use the highest-quality usable Hebrew transcript as source A and preserve its original metadata, text, timestamps, and whether it is manual or auto-generated. If no usable track exists, follow the configured, authorized audio-transcription fallback. Keep a provider transcript as an ASR draft, not ground truth. When the project requires comparing a YouTube transcript with source audio, preserve both independently and investigate material differences; do not automatically replace one with the other.

### Selection gate

Check the selected identity, chronology, eligibility, baseline, duplicate state, and existing-folder collision as separate criteria. Stop if any required result is below threshold. Create no new episode directory until selection passes.

## 2. Capture source and establish the episode record

Create a dated, slugged episode folder in the private project. Save the source item or transcript with provenance, but keep third-party article text in the private workspace. Verify the saved text against the retrieved source before drafting. Create a manifest from `schemas/episode-manifest.schema.json` and an empty append-only audit file from `schemas/jev-audit.schema.json`.

Record each atomic file creation, path, byte count, and SHA-256. Keep raw sources immutable. Put corrected or normalized versions in separate files with explicit parent hashes and reasons; never silently overwrite raw evidence. The public workflow repo gets only sanitized templates.

## 3. Extract claims and gather source evidence

The source-research agent processes one material claim at a time. For each claim, record:

- the article/video wording and source location or timestamp;
- whether it is a primary-source quotation, an author assertion, a historical statement, a current factual claim, or interpretation;
- the named primary source or authoritative current source;
- a compact exact excerpt, stable link, access time, and hash;
- what the source supports, what it does not establish, and remaining uncertainty.

Retrieve primary texts directly and verify citation identity, page/daf, wording, and context. For laws, current policies, prices, standards, or other changing facts, check a current authoritative source. Do not turn an author's claim into established fact merely because a cited text is adjacent to it. Do not copy long copyrighted passages into public artifacts.

After each retrieval, claim extraction, correction, or claim-to-source mapping, save the direct evidence and run separate Jev checks for source identity, quotation accuracy, relevance, attribution, and stated limit. Jev does not replace the direct source comparison.

## 4. Build the linear sugya

The linear-sugya editor orders the argument into a readable chain:

1. organizing question;
2. first primary source and its plain meaning;
3. the next source, tension, or qualification;
4. the author's application, kept clearly attributed;
5. the episode's limited inference and unresolved facts;
6. a practical resolution that does not exceed the sources.

Cover all material article themes or the full source lecture, not just the opening or most vivid claim. Make a coverage matrix linking every material source/claim to one outline move and then to one paragraph in each language. Check chronology, missing items, source order, and limits separately. Do not add an unrelated source to force a predetermined conclusion.

## 5. Write the Hebrew master

The Hebrew master is the content master. Draft in fluent rabbinic Hebrew from the approved source map and linear outline. Write one paragraph at a time; after each paragraph, save it, check its matching outline move, and gate its source claim, attribution, citation, qualification, and place in sequence as separate questions. Do not draft the next paragraph while a required check is unresolved.

Use Hebrew script for Hebrew names, religious vocabulary, titles, and citations. Daf references use Hebrew words and numerals, such as `דף מ״א עמוד א׳`. Keep quotations distinct from paraphrase and provide enough context to avoid misleading truncation. Do not issue a contemporary halachic ruling unless the episode's scope explicitly calls for one and the sources support it.

## 6. Translate to English with Luna Max

After a Hebrew paragraph passes its source and outline checks, send only that bounded paragraph (with its source-map entry and nearby transition context) to the Luna Max translator. Use `gpt-6-luna` with maximum reasoning. Translate Hebrew → English, paragraph by paragraph. Preserve paragraph count/order, claim scope, source sequence, uncertainty, and author attribution. Make the English idiomatic spoken prose, not a literal word-for-word rendering.

Keep every Hebrew-origin name, religious term, title, and daf citation in Hebrew script inside English. Put a fluent English translation immediately after each longer Hebrew quotation. Do not add facts, explanatory rulings, citations, or claims absent from the reviewed Hebrew master. A substantive ambiguity in Hebrew blocks translation until the Hebrew master is corrected and rechecked.

For each translated paragraph, check meaning, coverage, sequence, qualification, Hebrew-script vocabulary, citation form, and immediate quote translation separately. The next paragraph waits until all applicable checks pass.

## 7. Run the Hebrew-origin auditor

Audit every English paragraph, not a sample. The auditor flags Latin-script Hebrew-derived terms, names, prayers, source titles, rabbinic vocabulary, and Hebrew citations. It returns exact spans and Hebrew-script replacements without rewriting the prose. The editor applies only accepted corrections, records them, and reruns all affected paragraph checks and the auditor. Report zero remaining terms only after the full transcript has been inspected.

## 8. Write introductions and episode descriptions

Both spoken introductions and both written descriptions must include:

- the original source title and link;
- relevant primary-source links;
- reciprocal links to the English and Hebrew show/episode;
- an explicit AI-generated disclosure;
- whether a human reviewed the work (say plainly when no human review occurred);
- the actual model names used for drafting, translation, and audio generation.

Use the current values from the manifest. Never guess, shorten, or reuse old model names. Recheck model/provider information after the actual generation calls; if a model changed, correct every affected introduction/description and rerun the gates.

## 9. Generate audio

Use the locked per-language voice profiles and the current approved generation procedure. Never pick a fresh voice or silently fall back to another provider or model. Split only on paragraph boundaries unless the workflow explicitly validates another boundary scheme. Make every audio chunk a separate action, immediately record its request/response evidence, transcript hash, chunk index, model, voice, settings, seed if used, usage, provider-displayed cost, and artifact hash, then run its metadata and text-identity checks.

Assemble chunks from the approved manifest. Verify order, count, pauses, duration, codec, sample rate, channels, file size, transcript hashes, and final-file hash. Compare each language's assembled audio against its own approved transcript and confirm the two languages share the same source/outline coverage. Never regenerate a completed chunk silently; a new take is a new artifact with its own evidence and checks.

The current autonomous-release profile does not add manual listening as an extra gate unless the user's active instructions require it. Playback and public episode availability are still checked after publication.

## 10. Captions: conditional stage

The example profile sets captions to `paused`. In that state, do not call transcription or timestamping APIs for finished-podcast captions, create/validate SRT or VTT, or attach captions. Record “paused by user; no captions generated or attached,” and continue the other allowed stages. Do not modify historical caption artifacts.

Only after explicit user resumption and project-config update may the caption agent process the final audio. Use the approved transcription model, preserve raw response/provenance, build one SRT per language from the final audio, and validate SRT syntax, cue order, timing, overlap policy, language text, duration fit, encoding, and size. Check each independent criterion separately. Attach each transcript to its matching episode only if the service exposes that feature; read the saved attachment back. Do not report captions as attached from a local file alone.

## 11. Create and inspect artwork

Generate separate high-contrast square episode covers for the two languages. Keep episode art distinct from the permanent show covers and from each other; never change show-level art. Use readable Hebrew script, correct RTL layout, safe margins, clear focal image, and no fabricated quotations, logos, identifiable people, or misleading imagery.

For each cover, record the prompt, generation tool, date, output path, dimensions, and hash. Inspect spelling and visual composition at full size and phone-thumbnail size (for example 160×160); separately check title, language, dimensions, safe margins, legibility, and separation from show art. Keep failed generations and corrections in the audit without replacing the evidence.

## 12. Prepare and publish both editions

Confirm the active publication authorization. If not explicitly authorized for automatic publication, leave both editions in draft. If authorized, publish the English and Hebrew episodes to their configured existing shows only after all content, source, disclosure, audio, and artwork gates pass. Skip caption upload while captions are paused.

For each Spotify mutation, record the exact request, account/service result, and returned identifiers, then gate that one action. Reopen or refresh Creator details. Read title, description, language/show assignment, duration, saved episode art, and URL separately. Confirm that saved episode art matches the reviewed file and differs from the permanent show cover. Then verify the public episode page and playback. Listener surfaces may show show-level art; record that separately rather than mistaking it for failed Creator attachment.

If sign-in, browser access, local machine, source, or live readback fails, stop without bypassing authentication or claiming success. Preserve the item as `in_progress` and report the exact blocker.

## 13. Close out and resume safely

Only after both editions have live URLs, verified live records, and playable public pages, write the final ledger record as `published_bilingual`. Store the English and Hebrew episode URLs, final artifact hashes, caption status, Jev call count/confidence range, total usage, provider-displayed approximate cost, and any unavailable billing data. Gate the ledger write and read it back from disk as a separate action.

Leave the raw feed/source, source map, outline, masters, translations, audits, manifests, audio chunks, assembled audio, artwork prompts and final covers in the private dated folder. Public repo status, a Git commit, or a local artifact never substitutes for episode publication evidence.
