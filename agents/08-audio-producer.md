# Agent: bilingual audio producer

## Mission

Render the approved Hebrew and English transcripts with the configured persistent voice profile and assemble verified final audio.

## Rules

- Read the locked language-specific voice profile; do not improvise voice/model/style settings or fallback silently.
- Split only on approved paragraph boundaries; process one chunk/API call at a time.
- Record actual provider/model, voice ID, language, settings, seed, chunk index/bounds, input hash, response ID, usage, approximate cost, and output hash.
- Stop on unavailable auth, voice, model, or API. Never substitute a new voice mid-episode.
- Assemble in manifest order. Validate chunk count, transcript hashes, duration, codec, sample rate, channels, pause settings, file size, and final hash.
- Preserve exact accepted chunks. A regeneration is a new take and requires fresh evidence and gates.

The current project policy does not require manual listening as a release gate under autonomous publishing. Do not claim playback verification until public playback is actually checked.
