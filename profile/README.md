<p align="center">
  <a href="https://back2base.net"><img src="https://assets.back2base.net/brand/wordmark.svg" width="320" alt="back2base" /></a>
</p>

<p align="center">
  <a href="https://back2base.net"><strong>back2base.net</strong></a>
  &nbsp;·&nbsp;
  <a href="https://chat.back2base.net">chat</a>
  &nbsp;·&nbsp;
  <a href="https://github.com/Back2Base/oss-back2base">oss</a>
  &nbsp;·&nbsp;
  <a href="https://github.com/Back2Base/tones-oss">tones</a>
  &nbsp;·&nbsp;
  <a href="https://github.com/Back2Base/back2base-dist/releases">releases</a>
  &nbsp;·&nbsp;
  <a href="https://back2base.net/.well-known/security.txt">security</a>
</p>

---

Back2Base builds tools for working with [Claude Code](https://docs.anthropic.com/en/docs/claude-code).

## back2base

back2base runs Claude Code in a Docker container with a preconfigured set of MCP servers and an outbound firewall. It ships as a single binary and uses your existing Claude subscription. Nothing else needs to be installed on the host besides Docker.

There are two editions.

### Hosted ([back2base.net](https://back2base.net))

The CLI plus a backend that keeps your setup consistent across machines.

- Session memory stored in R2 and shared between devices
- Config and MCP profiles synced between devices
- Browser client at [`chat.back2base.net`](https://chat.back2base.net) using the same memory
- A managed `claudeproxy` gateway with shared rate limits and logging
- Sign-in through Auth0, linked to a Claude Pro, Max, Team, or Enterprise subscription

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

back2base login      # sign in and link your Claude subscription
back2base            # start Claude Code in the current directory
```

### Open source ([`oss-back2base`](https://github.com/Back2Base/oss-back2base))

The same container, firewall, and MCP servers without the hosted services. No account needed.

```sh
git clone https://github.com/Back2Base/oss-back2base
cd oss-back2base && go build -o oss-back2base .
./oss-back2base
```

| | `oss-back2base` | Hosted |
|---|:---:|:---:|
| Claude Code in a container | ✓ | ✓ |
| MCP server registry and profiles | ✓ | ✓ |
| Outbound firewall | ✓ | ✓ |
| Starter skills and slash commands | ✓ | ✓ |
| `claudeproxy` gateway | | ✓ |
| Config and memory sync | | ✓ |
| Browser client | | ✓ |
| Auth0 sign-in | | ✓ |

### What's in the container

- **MCP servers:** memory, sequential-thinking, brave-search, context7, lsmcp, git, fetch, sqlite, terraform, buildkite, datadog, and github.
- **Firewall:** `iptables` rules limit outbound traffic to Anthropic and an allowlist of other endpoints.
- **Image layout:** layers are ordered so the parts that change least come first, which keeps Anthropic's prompt cache warm between sessions.
- **Auth:** uses a Claude Pro, Max, Team, or Enterprise subscription through `claude setup-token`. No API key needed.

## Tones

[Tones](https://github.com/Back2Base/tones-oss) learns how you write from samples of your own writing and gives that to Claude over MCP, so drafts, docs, and code comments come out sounding like you instead of like a model. It runs on Cloudflare Workers, and each deployment belongs to one person: you host it on your own Cloudflare account and sign in through your own Auth0 tenant.

- Add samples by hand, or run the `collect_writing` prompt to have Claude find things you've written in Slack, email, Drive, Notion, GitHub, or local files. You approve each one before it's saved.
- Samples are grouped by register: `casual`, `professional`, `documentation`, `social`, and `general`.
- Tones builds a style profile for each register (sentence length, punctuation, vocabulary, phrasing, and so on) and rebuilds it as samples are added or deleted.
- `get_style_context` returns the profile plus a few matching excerpts for Claude to rewrite against. `get_comment_style` does the same for batches of code comments.

```sh
claude mcp add --transport http tones https://<your-domain>/mcp
```

Setup and deployment steps are in the [`tones-oss` README](https://github.com/Back2Base/tones-oss#readme).

## Repositories

| Repo | Visibility | Description |
|---|---|---|
| [`oss-back2base`](https://github.com/Back2Base/oss-back2base) | public | Open-source CLI and container |
| [`tones-oss`](https://github.com/Back2Base/tones-oss) | public | Tones MCP server for Cloudflare Workers |
| [`back2base`](https://github.com/Back2Base/back2base) | private | Hosted platform: CLI and Cloudflare Workers (landing, chat, config, proxy) |
| [`back2base-dist`](https://github.com/Back2Base/back2base-dist) | public | Hosted CLI release builds (tarballs, `.deb`, checksums) |
| [`homebrew-back2base`](https://github.com/Back2Base/homebrew-back2base) | public | Homebrew tap |
| [`apt-back2base`](https://github.com/Back2Base/apt-back2base) | public | APT repository |

## Contributing

Source for the hosted platform is private. Releases are built there and published to the public repos above. Pull requests for `oss-back2base` and `tones-oss` are welcome.

- Hosted platform: [discussions](https://github.com/Back2Base/back2base/discussions) and [issues](https://github.com/Back2Base/back2base/issues)
- `oss-back2base`: [issues](https://github.com/Back2Base/oss-back2base/issues)
- `tones-oss`: [issues](https://github.com/Back2Base/tones-oss/issues)

---

<sub>MIT licensed. Maintained by <a href="https://github.com/ramseymcgrath">@ramseymcgrath</a>.</sub>
