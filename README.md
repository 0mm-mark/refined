# refined

Grok Bot / Cursor plugin that connects to [Refine.ink](https://www.refine.ink) academic proofreading via the hosted MCP endpoint.

- MCP: `https://api.refine.ink/mcp`
- Same server as the [Claude Connectors Directory listing](https://claude.ai/directory/refine-ink)
- Docs: [https://www.refine.ink/developers](https://www.refine.ink/developers)
- Auth: OAuth by default (API keys also supported)

## What you get

| Piece | Role |
| --- | --- |
| `mcp.json` / `.mcp.json` | Points Cursor / Grok Bot at Refine's hosted MCP |
| `.cursor-plugin/plugin.json` | Authoritative Cursor plugin manifest |
| `.grok-plugin/plugin.json` | Thin Grok Bot compatibility mirror |
| `skills/refine-review/` | When and how to run a Refine review from chat |

No local server to run. The connector is a URL wrapper around Refine's remote MCP.

## Install

### Grok Bot (chat)

Ask your bot:

```text
Add a custom MCP server called refine at https://api.refine.ink/mcp
```

Confirm, then complete the OAuth connect card.

### Cursor team marketplace

Cursor Dashboard → Plugins → Import from Repo →
https://github.com/0mm-mark/refined

### Manual mcp.json

```json
{
  "mcpServers": {
    "refine": {
      "url": "https://api.refine.ink/mcp"
    }
  }
}
```

## Structure

```text
.cursor-plugin/plugin.json
.cursor-plugin/marketplace.json
.grok-plugin/plugin.json
.agents/plugins/marketplace.json
mcp.json
.mcp.json
skills/refine-review/SKILL.md
README.md
LICENSE
```

## License

MIT
