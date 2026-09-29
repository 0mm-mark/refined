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

In the bot that should use Refine, send:

```text
Add a custom MCP server called refine at https://api.refine.ink/mcp
```

The bot will confirm with a widget. Approve it, then complete the OAuth connect card (Refine account sign-in). Tools show up on the next message.

### Add to another Grok Bot

Yes. Connectors are added per chat: open the **other** bot and run the same install line there. Each bot that needs Refine should get its own add + OAuth once.

Steps:

1. Open the target bot in the Grok Bot sidebar (or Cmd-K).
2. Paste:

```text
Add a custom MCP server called refine at https://api.refine.ink/mcp
```

3. Confirm the add widget.
4. Finish the OAuth card when it appears.
5. Optional check: ask that bot `Is the refine connector connected?` or have it list MCP status.

You can also ask this Engineering Lead (or any bot with teammates) to message the target bot and start the add for you — name the bot, e.g. `Add refine to Researchy`. The target bot still needs you to approve its widget and OAuth card; another agent cannot complete those for you.

Do **not** paste API keys into chat. Prefer OAuth. If you must use an API key, create it in Refine Advanced Account Settings and tell the bot to add the server with an `X-API-Key` header — use a secret-request / secure input, never a chat paste.

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
