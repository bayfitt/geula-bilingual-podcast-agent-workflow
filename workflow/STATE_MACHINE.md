# Episode state machine

```mermaid
stateDiagram-v2
    [*] --> Discovered
    Discovered --> NoOp: not eligible / already published
    Discovered --> Queued: eligible and oldest unresolved
    Queued --> Captured: source identity and folder pass
    Captured --> Mapped: claim and source map pass
    Mapped --> Outlined: linear coverage passes
    Outlined --> HebrewDraft: Hebrew paragraphs pass
    HebrewDraft --> EnglishDraft: Luna Max paragraph pairs pass
    EnglishDraft --> LexicallyAudited: Hebrew-origin audit passes
    LexicallyAudited --> ReadyForMedia: disclosures and metadata pass
    ReadyForMedia --> AudioReady: both audio editions pass
    AudioReady --> CaptionsReady: captions explicitly resumed and pass
    AudioReady --> ArtworkReady: captions paused / stage skipped
    CaptionsReady --> ArtworkReady
    ArtworkReady --> ReadyToPublish: artwork checks pass
    ReadyToPublish --> Published: authorization + live service readback pass
    Discovered --> Blocked: identity, queue, or access failure
    Queued --> Blocked: Jev/source gate unresolved
    Captured --> Blocked
    Mapped --> Blocked
    Outlined --> Blocked
    HebrewDraft --> Blocked
    EnglishDraft --> Blocked
    LexicallyAudited --> Blocked
    ReadyForMedia --> Blocked
    AudioReady --> Blocked
    ArtworkReady --> Blocked
    ReadyToPublish --> Blocked
    Blocked --> Queued: resume exact first unresolved gate
    NoOp --> [*]
    Published --> [*]
```

`Blocked` is resumable, not terminal: keep evidence, ledger status, and artifacts. A failed gate never advances the state. A no-op creates no episode artifacts. Do not mark `Published` from a local upload result or draft folder.
