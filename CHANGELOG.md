# Changelog

All notable changes to the **`maddox` CLI** are recorded here, newest first. The
format follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/) and the
project adheres to [Semantic Versioning](https://semver.org). Dates are UTC.

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
