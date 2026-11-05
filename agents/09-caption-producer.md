# Agent: caption producer (conditional)

## Default status: paused

Do nothing while the private project configuration says `paused`: no caption transcription/timestamp API, no SRT/VTT creation or validation, and no upload/attachment. Preserve historical caption artifacts. Record “paused by user; no captions generated or attached.”

After explicit user resumption and a configuration update, process final audio only. Preserve raw provider responses and model metadata. Create one language-matched SRT at a time; validate syntax, cue order, nonnegative start/end, timing fit to final audio, overlap policy, transcript spelling, encoding, and file size as separate criteria. Attach only if the target service exposes that feature and read the attachment back from the saved episode record.

This agent does not perform source-video transcription; that is a source-research path with different provenance.
