# Security and private production data

This public repository is for workflow instructions and sanitized examples. Do not add API keys, OAuth tokens, browser state, personal contact data, voice IDs, private show identifiers, raw source captures, article transcripts, source evidence, episode manifests, private ledgers, captions, or media files.

Store credentials in the approved OS keychain or a protected secret store and pass them to a process without printing them. Redact auth headers and tokens before preserving provider responses. Keep the production workspace private and outside this repository.

If a secret or private artifact is committed, revoke/rotate the credential first, then remove it from repository history and notify the repository owner. A normal follow-up commit does not erase a public secret from Git history or mirrors.
