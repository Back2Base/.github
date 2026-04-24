<p align="center">
  <a href="https://back2base.net"><img src="https://assets.back2base.net/brand/wordmark.svg" width="320" alt="back2base" /></a>
</p>

<p align="center">
  <em>Containerized Claude Code, curated.</em>
</p>

<p align="center">
  <a href="https://back2base.net"><strong>back2base.net</strong></a>
  &nbsp;·&nbsp;
  <a href="https://chat.back2base.net">chat&nbsp;↗</a>
  &nbsp;·&nbsp;
  <a href="https://github.com/back2base/back2base/releases">releases</a>
  &nbsp;·&nbsp;
  <a href="https://back2base.net/.well-known/security.txt">security</a>
</p>

---

A Go CLI that launches [Claude&nbsp;Code](https://docs.anthropic.com/en/docs/claude-code) inside a hardened Docker container with a curated MCP bundle, network egress firewall, and prompt-cache optimizations. One binary, one container, zero host pollution.

## Install

```sh
# macOS
brew install back2base/back2base/back2base

# Linux (Debian/Ubuntu)
curl -fsSL https://back2base.github.io/apt-back2base/public.key \
  | sudo gpg --dearmor -o /usr/share/keyrings/back2base.gpg
echo "deb [signed-by=/usr/share/keyrings/back2base.gpg] \
  https://back2base.github.io/apt-back2base stable main" \
  | sudo tee /etc/apt/sources.list.d/back2base.list
sudo apt update && sudo apt install back2base

# First-time setup
back2base login      # Auth0 device flow + Claude subscription link
back2base            # launch Claude Code in the current project
```

Prefer the browser? **[chat.back2base.net](https://chat.back2base.net)** — the same memory stack, no install.

## Repositories

| Repo | Role |
|---|---|
| [`back2base`](https://github.com/back2base/back2base) | CLI + Cloudflare Workers (landing page, chat UI, config, proxy) — unified monorepo |
| [`back2base-dist`](https://github.com/back2base/back2base-dist) | Public release artifacts (tarballs, `.deb`, checksums) |
| [`homebrew-back2base`](https://github.com/back2base/homebrew-back2base) | Homebrew tap |
| [`apt-back2base`](https://github.com/back2base/apt-back2base) | APT repo + signed `Release` metadata |
| [`claudebox-memory`](https://github.com/back2base/claudebox-memory) | Cross-device session memory daemons + Cloudflare Worker |

## What you get

- **Curated MCP bundle** — memory, sequential-thinking, brave-search, context7, lsmcp, git, fetch, sqlite, terraform, buildkite, datadog, github
- **Network egress firewall** — `iptables` locks the container to Anthropic + an allow-listed set of endpoints
- **Cross-device memory** — every session's notes sync to R2; any other machine you log in on picks up where you left off
- **Prompt cache optimization** — container image layers sequenced for Anthropic's 5-minute cache TTL
- **Your Claude subscription** — Pro / Max / Team / Enterprise — billed through `claude setup-token`, no API keys required

## Contributing

Source lives in the private [`back2base`](https://github.com/back2base/back2base) repo by design — the build/release flow runs from there and artifacts land in the public repos above. Please [open a discussion](https://github.com/back2base/back2base/discussions) or [report an issue](https://github.com/back2base/back2base/issues) to engage.

---

<sub>MIT · designed by <a href="https://github.com/ramseymcgrath">@ramseymcgrath</a></sub>
