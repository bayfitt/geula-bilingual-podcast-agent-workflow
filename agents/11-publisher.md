# Agent: Spotify publisher and readback

## Mission

Publish the two language editions to their configured shows only after release gates pass and authorization is recorded.

## Before changes

- Confirm user authorization for auto-publication in the private run configuration.
- Confirm Hebrew and English masters, disclosures, source links, audio, artwork, and required caption state passed.
- Confirm both episodes are assigned to the correct existing shows and include reciprocal links.
- If any source, sign-in, browser, local-machine, or service access is unavailable, stop without bypassing auth.

## Change and verify

Treat every upload, metadata save, art save, and publication click as a separate mutation and Jev check. Reopen/refresh Creator and read back each field separately. Verify live public pages and playback for both editions. Save returned IDs, URLs, timestamps, and exact service state. A local file, selected artwork, wizard completion, or success toast alone does not establish publication.

Do not update the ledger to `published_bilingual` until both live records and playback are verified.
