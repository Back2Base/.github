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

## back2base

Claude Code in a Docker container with MCP servers and an outbound firewall. Uses your Claude subscription.

### Hosted ([back2base.net](https://back2base.net))

- Session memory synced across devices
- Config and MCP profiles synced across devices
- Browser client at [`chat.back2base.net`](https://chat.back2base.net)
- Managed `claudeproxy` gateway
- Auth0 sign-in

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

back2base login
back2base
```

### Open source ([`oss-back2base`](https://github.com/Back2Base/oss-back2base))

Same container without the hosted services. No account needed.

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

### Container

- **MCP servers:** memory, sequential-thinking, brave-search, context7, lsmcp, git, fetch, sqlite, terraform, buildkite, datadog, github
- **Firewall:** `iptables` allowlist for outbound traffic
- **Image layers:** ordered for prompt caching
- **Auth:** Claude Pro, Max, Team, or Enterprise via `claude setup-token`

## Tones

[Tones](https://github.com/Back2Base/tones-oss) is an MCP server that learns your writing style from samples. Claude uses it to write in your voice. Self-hosted on Cloudflare Workers with Auth0 sign-in.

- Add samples directly or with the `collect_writing` prompt
- Separate profiles for `casual`, `professional`, `documentation`, `social`, and `general`
- `get_style_context` for prose, `get_comment_style` for code comments

```sh
claude mcp add --transport http tones https://<your-domain>/mcp
```

See the [`tones-oss` README](https://github.com/Back2Base/tones-oss#readme) for setup.

## Repositories

| Repo | Visibility | Description |
|---|---|---|
| [`oss-back2base`](https://github.com/Back2Base/oss-back2base) | public | Open-source CLI and container |
| [`tones-oss`](https://github.com/Back2Base/tones-oss) | public | Tones MCP server |
| [`back2base`](https://github.com/Back2Base/back2base) | private | Hosted platform |
| [`back2base-dist`](https://github.com/Back2Base/back2base-dist) | public | Hosted CLI releases |
| [`homebrew-back2base`](https://github.com/Back2Base/homebrew-back2base) | public | Homebrew tap |
| [`apt-back2base`](https://github.com/Back2Base/apt-back2base) | public | APT repository |

## Contributing

PRs welcome on [`oss-back2base`](https://github.com/Back2Base/oss-back2base) and [`tones-oss`](https://github.com/Back2Base/tones-oss). For the hosted platform, use [discussions](https://github.com/Back2Base/back2base/discussions) or [issues](https://github.com/Back2Base/back2base/issues).

---

<sub>MIT licensed. Maintained by <a href="https://github.com/ramseymcgrath">@ramseymcgrath</a>.</sub>
