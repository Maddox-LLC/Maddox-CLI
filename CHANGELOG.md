# Changelog

All notable changes to the **`maddox` CLI** are recorded here, newest first. The
format follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/) and the
project adheres to [Semantic Versioning](https://semver.org). Dates are UTC.

## [0.3.0] - 2026-07-01

### Added
- Update notifications — `maddox` now tells you when a newer version is available,
  e.g. `maddox 0.3.0 is available (you have 0.2.0) — upgrade with: brew upgrade maddox`.
  The check runs at most once a day, only in an interactive terminal (never in
  scripts, pipes, or CI), and never slows a command (500ms timeout, fully offline-safe).
  Silence it with `MADDOX_NO_UPDATE_CHECK=1`; `NO_COLOR` is honored.

## [0.2.0] - 2026-06-30

### Added
- `maddox labels batch` — render many labels in one call from an items JSON file (or
  stdin): pass a `{ "items": [...] }` object or a bare array of render bodies (each
  item is a `labels create` body — `template_id` + `--field`/`--value` equivalents,
  plus an optional `external_ref`). Prints a per-item table and a
  `total / ok / failed` summary; `--output-dir <dir>` downloads each successful PNG
  (named by `external_ref`, else content hash); `--json` emits machine-readable
  results; exits non-zero if any item failed.

## [0.1.0] - 2026-06-28

Initial release.

### Added
- `maddox signup`, `login`, `whoami`, `config` — create a tenant, store an API key
  (with named profiles), and check the identity behind the current key.
- `maddox labels render` — render raw ZPL to a PNG from a file or stdin, with
  `--source-dpi` / `--target-dpi`, `--threshold`, and `--font-profile` options.
- `maddox labels create` — render a registry template, hydrated with `--value`
  (`^FN`) or semantic `--field` values.
- `maddox labels list` / `get` / `input` — browse rendered labels and download a
  PNG by its content hash.
- `maddox templates list` / `get` / `commit` / `delete` / `synthesize` — manage
  label templates, including AI synthesis of a draft from legacy ZPL.
- `maddox keys list` / `create` / `revoke` / `update` — manage tenant API keys.
- `maddox usage` — show the tenant's plan usage and limits.
- `maddox lint` — lint ZPL offline, with no network or API key required.
- `--json` machine-readable output and `--profile` selection across commands.
- Prebuilt static binaries for macOS (arm64/x86_64), Linux (arm64/x86_64, musl),
  and Windows (x86_64), distributed via a Homebrew tap and a checksum-verified
  `install.sh`.
