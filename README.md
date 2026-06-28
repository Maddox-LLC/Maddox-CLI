# maddox

[![Release](https://img.shields.io/github/v/release/Maddox-LLC/maddox?display_name=tag&sort=semver&label=release)](https://github.com/Maddox-LLC/maddox/releases)
[![Homebrew](https://img.shields.io/badge/homebrew-maddox--llc%2Fmaddox-orange)](https://github.com/Maddox-LLC/homebrew-maddox)
[![License: MIT](https://img.shields.io/badge/license-MIT-blue)](#license)

Puts the [Maddox API](https://api.maddoxapi.dev) in your terminal — render ZPL
labels to PNG, manage templates and API keys, and lint ZPL offline, all from the
command line. A single static binary, no runtime dependencies.

## Documentation

Full API docs live in the [Maddox Console](https://app.maddoxapi.dev). Run
`maddox <command> --help` for command-level reference.

## Installation

### Homebrew

```sh
brew install maddox-llc/maddox/maddox
```

### curl | sh

Downloads the binary for your platform, verifies its SHA-256, and installs to
`~/.local/bin` (override with `--dir`):

```sh
curl -fsSL https://raw.githubusercontent.com/Maddox-LLC/maddox/main/install.sh | sh
```

### Manual

Grab the binary for your platform from the
[latest release](https://github.com/Maddox-LLC/maddox/releases/latest), verify it
against `SHA256SUMS`, `chmod +x`, and put it on your `PATH`.

## Getting started

Authenticate, then run your first command:

```sh
# New here? Create a tenant — prints an API key once, and stores it locally.
maddox signup --email you@example.com --save

# Already have a key? Store it (written to ~/.maddox/credentials, 0600):
maddox login --api-key mdx_...
# …or pass it ephemerally via the environment:
export MADDOX_API_KEY=mdx_...

maddox whoami
```

## Usage

Commands follow `maddox <group> <action> [options]`. Add `--json` to any command
for machine-readable output, and `--help` anywhere for details.

```sh
# Render raw ZPL to a PNG
maddox labels render --zpl label.zpl -o label.png
echo '^XA^FO50,50^A0N,40^FDHello^FS^XZ' | maddox labels render -o label.png

# Render a registry template hydrated with semantic fields
maddox labels create --template asset-tag --field asset_id=MER-04821 -o tag.png

# Lint ZPL offline — no network, no key required
maddox lint label.zpl

# List and fetch rendered labels
maddox labels list
maddox labels get <hash> -o label.png

# Manage templates
maddox templates list
maddox templates get <id>

# Keys and usage
maddox keys create --label "ci-runner"
maddox usage
maddox usage --json | jq .
```

## Configuration

Credentials and settings live in `~/.maddox/credentials` (TOML, `0600`). Manage
them with `maddox config`, and keep separate environments in named profiles:

```sh
maddox config set api_key mdx_... --profile sandbox
maddox config set base_url https://api.maddoxapi.dev
maddox config list                 # every profile, values masked
maddox --profile sandbox whoami    # use a profile for one command
maddox config path                 # where the file lives
```

Resolution order for the key and base URL: the `--api-key` / `--base-url` flag (or
its `MADDOX_API_KEY` / `MADDOX_BASE_URL` env var) → the active profile → built-in
default.

## Exit codes

| Code | Meaning |
| --- | --- |
| `0` | success |
| `1` | local / usage error (bad flags, missing credentials, file not found) |
| `2` | API error (the request reached Maddox and was rejected) |

## Requirements

Prebuilt static binaries are published for:

- macOS — Apple Silicon (`arm64`) and Intel (`x86_64`)
- Linux — `arm64` and `x86_64` (static musl, no glibc dependency)
- Windows — `x86_64` (download the `.exe` from Releases)

## About this repo

This is the **distribution** repo — it hosts the released binaries, their
`SHA256SUMS`, and the `install.sh` installer. The CLI source lives in the private
Maddox monorepo; the Homebrew formula lives in the
[`homebrew-maddox`](https://github.com/Maddox-LLC/homebrew-maddox) tap.

## License

[MIT](https://opensource.org/license/mit).
