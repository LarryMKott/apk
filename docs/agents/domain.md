# Domain Docs

How the engineering skills should consume this repo's domain documentation when exploring the codebase.

## Layout

**multi-context** — a root `GLOSSARY-MAP.md` points at one `GLOSSARY.md` per context, and each context may carry its own `docs/adr/` for context-scoped decisions. System-wide decisions stay in `docs/adr/` at the repo root.

The contexts in this repo are the three OpenWrt package channels under `run/`:

- `run/arm64` — `aarch64_generic` packages
- `run/arm64-a53` — `aarch64_cortex-a53` packages
- `run/x86` — `x86_64` packages

Neither `GLOSSARY-MAP.md` nor any per-context `GLOSSARY.md` exists yet: they are created lazily by `/domain-modeling` the first time a term or decision is actually written down. Until then, proceed silently — see below.

If an older `CONTEXT.md` or `CONTEXT-MAP.md` shows up anywhere in this repo, it is the previous name of `GLOSSARY.md` / `GLOSSARY-MAP.md`: read it as the glossary, and rename it the next time that file is edited.

## Before exploring, read these

- **`GLOSSARY-MAP.md`** at the repo root: it points at one `GLOSSARY.md` per context. Read each one relevant to the topic.
- **`GLOSSARY.md`** at the repo root, for terms shared across all contexts (if present).
- **`docs/adr/`**: read ADRs that touch the area you're about to work in. Also check `run/<context>/docs/adr/` for context-scoped decisions.

If any of these files don't exist, **proceed silently**. Don't flag their absence; don't suggest creating them upfront. The `/domain-modeling` skill (reached via `/grill-with-docs` and `/improve-codebase-architecture`) creates them lazily when terms or decisions actually get resolved.

## File structure

```
/
├── GLOSSARY-MAP.md                    ← created on first term; points at each context
├── docs/adr/                          ← system-wide decisions
└── run/
    ├── arm64/
    │   ├── GLOSSARY.md                ← created on first term for this context
    │   └── docs/adr/                  ← context-specific decisions
    ├── arm64-a53/
    │   ├── GLOSSARY.md
    │   └── docs/adr/
    └── x86/
        ├── GLOSSARY.md
        └── docs/adr/
```

## Use the glossary's vocabulary

When your output names a domain concept (in an issue title, a refactor proposal, a hypothesis, a test name), use the term as defined in `GLOSSARY.md`. Don't drift to synonyms the glossary explicitly avoids.

If the concept you need isn't in the glossary yet, that's a signal: either you're inventing language the project doesn't use (reconsider) or there's a real gap (note it for `/domain-modeling`).

## Flag ADR conflicts

If your output contradicts an existing ADR, surface it explicitly rather than silently overriding:

> _Contradicts ADR-0007 (event-sourced orders), but worth reopening because…_
