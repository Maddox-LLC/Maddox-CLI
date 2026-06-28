# maddox

Official command-line interface for the **Maddox API** (`maddox`).

```sh
# Homebrew
brew install maddox-llc/maddox/maddox

# or curl | sh
curl -fsSL https://raw.githubusercontent.com/Maddox-LLC/maddox/main/install.sh | sh

maddox --version
```

## What's here

This is the **distribution** repo — it hosts the released binaries
(under [Releases](https://github.com/Maddox-LLC/maddox/releases)), their
`SHA256SUMS`, and the `install.sh` installer. The CLI source lives in the private
Maddox monorepo; the Homebrew formula lives in the
[`homebrew-maddox`](https://github.com/Maddox-LLC/homebrew-maddox) tap.

## Install details

- `install.sh` detects your OS/arch, downloads the matching binary from the
  latest (or a pinned `MADDOX_VERSION`) release, **verifies its SHA-256** against
  `SHA256SUMS`, and installs to `~/.local/bin` (override with `--dir`).
- Platforms: macOS (arm64/x86_64), Linux (arm64/x86_64, static musl), Windows
  (x86_64 — download the `.exe` from Releases).

## License

MIT.
