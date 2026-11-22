# kit-cli-app

Build CLI applications in handl — a `kit.hnl` v1 curation manifest over
`lib-*` packages (proposal P-004): argv parsing (`mri`), standard
streams (`stdio`/`stdio-c`), POSIX fs/env/time (`posix-c`), child
processes (`cli`), JSON, strings, and collections.

## Manifest

`kit.hnl` is a pure curation manifest — `{ name, description, license,
libs }` only. No plugins, no entry/glue (kit.hnl v1, user-approved
2026-11-22).

**`libs` convention:** each entry is a lib *package* name — the `lib-*`
GitHub repo name minus the `lib-` prefix (e.g. `lib-mri` → `"mri"`,
`lib-stdio-c` → `"stdio-c"`). Resolution goes through each package's own
`pkg.hnl`: its `modules` declare what it ships and its `deps` pull
contracts and transitive backends, so the kit lists the curated set, not
the closure.

Notes vs the P-004 sketch:

- `args` → **`mri`**: `lib-args` does not exist yet; `lib-mri` ships an
  argv parser (npm mri semantics) as module `mri`.
- `time-c` → dropped: `lib-time`/`lib-time-c` were folded into the posix
  family; `lib-posix-c` implements `now_ms`/`instant_ns`/`epoch` via a
  direct `clock_gettime` `ffi.call`.
- `stdio` needed both halves: `lib-stdio` (contract) + `lib-stdio-c`
  (libc backend via `ffi.call`).

## Layout

```text
kit.hnl   the curation manifest (the whole repo)
```

## Gate

None yet — no `hnl` binary is available to validate `kit.hnl` parses.
When the kit.hnl loader lands (host-side or pkg), a parse/lint gate can
be added (`scripts/hnl-gate.sh` pattern from the `lib-*` repos).

## License

MIT.
