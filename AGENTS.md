# kit-cli-app

Build CLI applications in handl — a `kit.hnl` v1 curation manifest over
`lib-*` packages (proposal P-004): argv parsing (`mri`), standard
streams (`stdio`/`stdio-c`), POSIX fs/env/time (`posix-c`), child
processes (`cli`), JSON, strings, and collections.

## Layout

| path | role |
| --- | --- |
| `kit.hnl` | the kit.hnl v1 curation manifest — the whole repo |
| `workflows/` | bupha gate wiring |

## Contract

- `kit.hnl` is pure curation — `{ name, description, license, libs }`
  only; no plugins, no entry/glue (kit.hnl v1, user-approved
  2026-11-22).
- **`libs` convention:** each entry is a lib *package* name — the
  `lib-*` repo name minus the `lib-` prefix (`lib-mri` → `"mri"`).
  Resolution goes through each package's own `pkg.hnl`: `modules`
  declare what it ships, `deps` pull contracts and transitive backends
  — the kit lists the curated set, not the closure.

## Verification

Manifest-only repo — no build. The kit resolves through the consuming
runtime's kit machinery (`hnl` + sibling `lib-*` checkouts).

<!-- myco:agent-awareness -->

## Agent awareness

- Session start / any work discussion: run `myco status --prompt`
  before proposing next steps — know the board first.
- User describes new work → offer to capture it (`myco todo add`,
  `issue new`, `proposal new`). Don't wait to be asked.
- Picking up a task: `myco resume <ID>` is the briefing.
- Wrapping up: `myco handoff <ID>` anything resumable; keep statuses
  honest (claimed → in-progress → blocked/done).

<!-- /myco:agent-awareness -->
