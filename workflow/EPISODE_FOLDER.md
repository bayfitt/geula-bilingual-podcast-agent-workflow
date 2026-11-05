# Private episode-folder layout

Use one dated folder per source item. A recommended ID is `YYYY-MM-DD-<short-source-slug>`; add a stable source ID where needed to prevent collisions. Keep the folder in the private production workspace, never in this public workflow repository.

```text
episodes/YYYY-MM-DD-source-slug/
├── manifest.json
├── source/
│   ├── selected-feed-item.json
│   └── raw-transcript.json        # video path only; preserve provider metadata
├── evidence/
│   ├── source-claim-0001.txt
│   └── jev-audit.jsonl            # append-only
├── source-map.md
├── linear-outline.md
├── master-he.txt                  # authoritative spoken transcript
├── translation-en.txt             # paragraph-aligned Luna Max output
├── descriptions/
│   ├── he.txt
│   └── en.txt
├── audio/
│   ├── he/chunks/                 # one record per request and output
│   ├── en/chunks/
│   ├── final-he.<codec>
│   └── final-en.<codec>
├── artwork/
│   ├── cover-he.png
│   └── cover-en.png
└── captions/                      # only if explicitly enabled
    ├── he.srt
    └── en.srt
```

Do not create caption files or make the `captions/` directory while captions are paused. Preserve raw source, corrected transcript, final master, and generated media as separate artifacts. Never rewrite `jev-audit.jsonl`; append every call, including failures and retries. Store full source captures only when needed and permitted; a stable URL, exact excerpt, timestamp, and hash may be sufficient evidence.
