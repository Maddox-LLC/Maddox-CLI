# Maddox-CLI

[![Release](https://img.shields.io/github/v/release/Maddox-LLC/Maddox-CLI?display_name=tag&sort=semver&label=release)](https://github.com/Maddox-LLC/Maddox-CLI/releases)
[![Homebrew](https://img.shields.io/badge/homebrew-maddox--llc%2Ftap-orange)](https://github.com/Maddox-LLC/homebrew-tap)
[![License: MIT](https://img.shields.io/badge/license-MIT-blue)](#license)

The official command-line interface for the [Maddox API](https://api.maddoxapi.dev).
Render ZPL to PNG, manage label templates and API keys, inspect usage and limits,
and lint ZPL offline — all without leaving your terminal. It ships as a single
static binary with no runtime dependencies.

## Documentation

Complete API and product documentation is available at
**[Maddox Docs](https://docs.maddoxapi.dev)**. For command-level reference, run
`maddox <command> --help`.

## Installation

### Homebrew

```sh
brew install maddox-llc/tap/maddox
```

### curl

The installer downloads the binary for your platform, verifies its SHA-256
checksum, and installs it to `~/.local/bin` (override with `--dir`):

```sh
curl -fsSL https://raw.githubusercontent.com/Maddox-LLC/Maddox-CLI/main/install.sh | sh
```

### Manual

Download the binary for your platform from the
[latest release](https://github.com/Maddox-LLC/Maddox-CLI/releases/latest), verify it
against `SHA256SUMS`, mark it executable (`chmod +x`), and place it on your `PATH`.

## Getting started

Authenticate once, then run your first command:

```sh
# New to Maddox? Create a tenant. Your API key is shown once and saved locally.
maddox signup --email you@example.com --save

# Already have a key? Store it (written to ~/.maddox/credentials, mode 0600):
maddox login --api-key mdx_live_...

# Or supply it through the environment for a single session:
export MADDOX_API_KEY=mdx_live_...

maddox whoami
```

## Usage

Commands follow the pattern `maddox <group> <action> [options]`. Append `--json`
to any command for machine-readable output, or `--help` for full details.

```sh
# Render raw ZPL to a PNG
maddox labels render --zpl label.zpl -o label.png
echo '^XA^FO50,50^A0N,40^FDHello^FS^XZ' | maddox labels render -o label.png

# Render a registry template, hydrated with semantic fields
maddox labels create --template asset-tag --field asset_id=MER-04821 -o tag.png

# Lint ZPL offline — no network or API key required
maddox lint label.zpl

# List and download previously rendered labels
maddox labels list
maddox labels get <hash> -o label.png

# Manage label templates
maddox templates list
maddox templates get <id>

# Inspect API keys and usage
maddox keys create --label "ci-runner"
maddox usage
maddox usage --json | jq .
```

## Configuration

Credentials and settings are stored in `~/.maddox/credentials` (TOML, mode
`0600`). Manage them with `maddox config`, and keep environments separate using
named profiles:

```sh
maddox config set api_key mdx_live_... --profile sandbox
maddox config set base_url https://api.maddoxapi.dev
maddox config list                 # all profiles, with values masked
maddox --profile sandbox whoami    # use a profile for a single command
maddox config path                 # print the credentials file location
```

The API key and base URL are resolved in this order: the `--api-key` /
`--base-url` flag (or its `MADDOX_API_KEY` / `MADDOX_BASE_URL` environment
variable), then the active profile, then the built-in default.

## Exit codes

| Code | Meaning |
| --- | --- |
| `0` | Success |
| `1` | Local or usage error (invalid flags, missing credentials, file not found) |
| `2` | API error (the request reached Maddox and was rejected) |

## Requirements

Prebuilt static binaries are published for:

- **macOS** — Apple Silicon (`arm64`) and Intel (`x86_64`)
- **Linux** — `arm64` and `x86_64` (static musl; no glibc dependency)
- **Windows** — `x86_64` (download the `.exe` from the releases page)

## About this repository

This is the **distribution** repository: it hosts the released binaries, their
`SHA256SUMS`, and the `install.sh` installer. The CLI source is maintained in
Maddox's private monorepo, and the Homebrew formula lives in the
[`homebrew-tap`](https://github.com/Maddox-LLC/homebrew-tap) repository.

## License

Released under the [MIT License](https://opensource.org/license/mit).
