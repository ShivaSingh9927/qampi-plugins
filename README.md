# Qampi plugins

Run LinkedIn outreach from your coding agent with [Qampi](https://qampi.com).
Find prospects, add them as leads, start a campaign and see who replied,
without leaving Claude Code or Codex.

You need a Qampi account with LinkedIn connected and an API key
(**Settings → API keys** in the Qampi app).

## Claude Code

```bash
claude plugin marketplace add ShivaSingh9927/qampi-plugins
claude plugin install qampi@qampi
```

Claude Code asks for your API key when the plugin is enabled and keeps it in
your system's secure credential store. You can also pick the mode there.

## Codex

```bash
codex plugin marketplace add ShivaSingh9927/qampi-plugins
```

Then install **Qampi** from the plugin directory in Codex.

Codex plugins can't ask for a key yet, so save it once in a file:

```bash
mkdir -p ~/.config/qampi
printf '%s' 'qampi_live_your_key_here' > ~/.config/qampi/api-key
chmod 600 ~/.config/qampi/api-key
```

The Codex plugin runs in read-only mode. To let Codex add leads and run
campaigns, add the server to `~/.codex/config.toml` yourself instead:

```toml
[mcp_servers.qampi]
command = "npx"
args = ["-y", "@qampi/mcp-server"]
env = { QAMPI_MODE = "full" }
```

## Modes

| Mode | What the agent can do |
|---|---|
| `read-only` (default) | Look at your account, leads, campaigns and results. Nothing that changes anything is even visible to the agent. |
| `full` | Also add leads, create campaigns, find emails and, after you say yes, launch campaigns. |

Launching a campaign contacts real people and can't be undone, so the agent
must get an explicit yes from you first.

## What's inside

- `plugins/qampi/` — the plugin: the [Qampi MCP server](https://www.npmjs.com/package/@qampi/mcp-server)
  plus a skill that teaches the agent the safe order of work.
- `.claude-plugin/marketplace.json` — the Claude Code marketplace.
- `.agents/plugins/marketplace.json` — the Codex marketplace.

The MCP server is also listed in the [MCP Registry](https://registry.modelcontextprotocol.io)
as `io.github.ShivaSingh9927/qampi`, for any other MCP client.
