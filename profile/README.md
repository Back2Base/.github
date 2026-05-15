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
  <a href="https://github.com/Back2Base/oss-back2base">oss</a>
  &nbsp;·&nbsp;
  <a href="https://github.com/Back2Base/back2base-dist/releases">releases</a>
  &nbsp;·&nbsp;
  <a href="https://back2base.net/.well-known/security.txt">security</a>
</p>

---

**back2base** runs [Claude&nbsp;Code](https://docs.anthropic.com/en/docs/claude-code) inside a hardened Docker container with a curated MCP bundle, an outbound egress firewall, and prompt-cache–optimized layering. One binary, one container, zero host pollution — your Claude subscription, sandboxed.

## Two ways to run it

### 🚀 [back2base.net](https://back2base.net) — the hosted platform

The full experience. CLI + a managed backend so your Claude Code setup follows you across machines.

- Cross-device session memory (R2-backed, picks up where you left off)
- Config + MCP profiles synced across devices
- [`chat.back2base.net`](https://chat.back2base.net) — browser access, same memory stack, no install
- Managed `claudeproxy` gateway with shared rate limits and observability
- Auth0 sign-in linked to your Claude Pro / Max / Team / Enterprise subscription

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

back2base login      # Auth0 device flow + Claude subscription link
back2base            # launch Claude Code in the current project
```

### 🛠 [`oss-back2base`](https://github.com/Back2Base/oss-back2base) — the open-source slice

Same container runtime, same firewall, same MCP bundle — no hosted services, no account required. Build from source, run anywhere Docker runs.

```sh
git clone https://github.com/Back2Base/oss-back2base
cd oss-back2base && go build -o oss-back2base .
./oss-back2base
```

| Feature | `oss-back2base` | [back2base.net](https://back2base.net) |
|---|:---:|:---:|
| Containerized Claude Code | ✓ | ✓ |
| Curated MCP server registry + profiles | ✓ | ✓ |
| Outbound iptables firewall | ✓ | ✓ |
| Starter skills + slash commands | ✓ | ✓ |
| Managed `claudeproxy` gateway | — | ✓ |
| Cross-device config + memory sync | — | ✓ |
| Browser app (`chat.back2base.net`) | — | ✓ |
| Auth0 sign-in | — | ✓ |

## What's in the container

- **Curated MCP bundle** — memory, sequential-thinking, brave-search, context7, lsmcp, git, fetch, sqlite, terraform, buildkite, datadog, github
- **Network egress firewall** — `iptables` locks the container to Anthropic + an allow-listed set of endpoints
- **Prompt cache optimization** — image layers sequenced for Anthropic's 5-minute cache TTL
- **Your Claude subscription** — Pro / Max / Team / Enterprise — via `claude setup-token`, no API keys required

## Repositories

| Repo | Visibility | Role |
|---|---|---|
| [`oss-back2base`](https://github.com/Back2Base/oss-back2base) | public | Open-source CLI + container runtime |
| [`back2base`](https://github.com/Back2Base/back2base) | private | Hosted platform monorepo — CLI + Cloudflare Workers (landing, chat, config, proxy) |
| [`back2base-dist`](https://github.com/Back2Base/back2base-dist) | public | Release artifacts for the hosted CLI (tarballs, `.deb`, checksums) |
| [`homebrew-back2base`](https://github.com/Back2Base/homebrew-back2base) | public | Homebrew tap |
| [`apt-back2base`](https://github.com/Back2Base/apt-back2base) | public | APT repo + signed `Release` metadata |

## Contributing

The hosted-platform source lives in the private [`back2base`](https://github.com/Back2Base/back2base) repo by design — the build/release flow runs from there and artifacts land in the public repos above. For the OSS runtime, contribute directly to [`oss-back2base`](https://github.com/Back2Base/oss-back2base).

- Hosted platform questions → [discussions](https://github.com/Back2Base/back2base/discussions) · [issues](https://github.com/Back2Base/back2base/issues)
- OSS runtime → [`oss-back2base` issues](https://github.com/Back2Base/oss-back2base/issues)

---

<sub>MIT · <a href="https://back2base.net">back2base.net</a> · designed by <a href="https://github.com/ramseymcgrath">@ramseymcgrath</a></sub>
