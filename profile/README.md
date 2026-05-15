<p align="center">
  <a href="https://back2base.net"><img src="https://assets.back2base.net/brand/wordmark.svg" width="320" alt="back2base" /></a>
</p>

<p align="center">
  <em>Containerized Claude Code, curated.</em>
</p>

<p align="center">
  <a href="https://back2base.net"><strong>back2base.net</strong></a>
  &nbsp;·&nbsp;
  <a href="https://chat.back2base.net">chat</a>
  &nbsp;·&nbsp;
  <a href="https://github.com/Back2Base/oss-back2base">oss</a>
  &nbsp;·&nbsp;
  <a href="https://github.com/Back2Base/back2base-dist/releases">releases</a>
  &nbsp;·&nbsp;
  <a href="https://back2base.net/.well-known/security.txt">security</a>
</p>

---

**back2base** runs [Claude&nbsp;Code](https://docs.anthropic.com/en/docs/claude-code) inside a hardened Docker container with a curated MCP bundle, an outbound egress firewall, and prompt-cache–optimized image layering. A single binary, a single container, and no host-level dependencies — your Claude subscription, sandboxed.

## Editions

### [back2base.net](https://back2base.net) — hosted platform

The CLI plus a managed backend, so your Claude Code environment follows you across machines.

- Cross-device session memory backed by R2
- Configuration and MCP profiles synchronized across devices
- Browser client at [`chat.back2base.net`](https://chat.back2base.net) — same memory stack, no install required
- Managed `claudeproxy` gateway with shared rate limits and observability
- Auth0 sign-in linked to your Claude Pro, Max, Team, or Enterprise subscription

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

### [`oss-back2base`](https://github.com/Back2Base/oss-back2base) — open-source runtime

The same container runtime, firewall, and MCP bundle, without the hosted services. No account required. Builds from source and runs anywhere Docker runs.

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

- **Curated MCP bundle.** memory, sequential-thinking, brave-search, context7, lsmcp, git, fetch, sqlite, terraform, buildkite, datadog, and github.
- **Network egress firewall.** `iptables` rules restrict the container to Anthropic and an allow-listed set of endpoints.
- **Prompt cache optimization.** Image layers are sequenced for Anthropic's 5-minute cache TTL.
- **Subscription-based auth.** Pro, Max, Team, and Enterprise accounts via `claude setup-token`; no API keys required.

## Repositories

| Repo | Visibility | Role |
|---|---|---|
| [`oss-back2base`](https://github.com/Back2Base/oss-back2base) | public | Open-source CLI + container runtime |
| [`back2base`](https://github.com/Back2Base/back2base) | private | Hosted platform monorepo — CLI + Cloudflare Workers (landing, chat, config, proxy) |
| [`back2base-dist`](https://github.com/Back2Base/back2base-dist) | public | Release artifacts for the hosted CLI (tarballs, `.deb`, checksums) |
| [`homebrew-back2base`](https://github.com/Back2Base/homebrew-back2base) | public | Homebrew tap |
| [`apt-back2base`](https://github.com/Back2Base/apt-back2base) | public | APT repo + signed `Release` metadata |

## Contributing

The hosted-platform source resides in the private [`back2base`](https://github.com/Back2Base/back2base) repository by design; the build and release pipeline runs from there, and artifacts are published to the public repositories above. Contributions to the open-source runtime are welcome directly in [`oss-back2base`](https://github.com/Back2Base/oss-back2base).

- Hosted platform: [discussions](https://github.com/Back2Base/back2base/discussions) and [issues](https://github.com/Back2Base/back2base/issues)
- Open-source runtime: [`oss-back2base` issues](https://github.com/Back2Base/oss-back2base/issues)

---

<sub>MIT licensed. <a href="https://back2base.net">back2base.net</a>. Maintained by <a href="https://github.com/ramseymcgrath">@ramseymcgrath</a>.</sub>
