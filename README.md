# Stopover MCP server

Stopover ([flystopover.com](https://flystopover.com)) plans multi-city trips: the cheapest order of cities, the dates, and the flights or trains between them.

This repo holds the docs for Stopover's remote MCP server, so you can use it from Claude, ChatGPT, Cursor, VS Code and other MCP clients. There is no code to install or run. The server is hosted.

| | |
|---|---|
| Endpoint | `https://mcp.flystopover.com/mcp` |
| Transport | Streamable HTTP |
| Auth | None needed for planning |
| Price | Free |
| Official MCP Registry | `com.flystopover/stopover` |
| Claude directory | [claude.ai/directory/connectors/stopover](https://claude.ai/directory/connectors/stopover) |

Not to be confused with other projects that use the name "stopover". This one is the trip planner at flystopover.com.

## Tools

**plan_trip** plans a trip. Give it a home airport, 1 to 7 cities and a date window. It finds the order of cities and the dates that cost least, with flights or trains for each leg and booking links.

**get_plan** reads a plan you already made, by its id.

### Example prompts

- "Use Stopover to plan a trip from Dallas to Lisbon, Madrid and Paris between May 4 and May 20, 2027."
- "Plan a trip from Chicago to Rome, Florence and Venice in September 2027 with Stopover. What order is cheapest?"
- "With Stopover, find the cheapest way to see Tokyo, Osaka and Seoul from Los Angeles, leaving after March 10, 2027 and back by March 28."
- "Show me Stopover plan <plan id> again, leg by leg." (uses get_plan)

## Add it to your client

### Claude (claude.ai and Claude Desktop)

Easiest: open the directory listing at [claude.ai/directory/connectors/stopover](https://claude.ai/directory/connectors/stopover) and click Connect.

Or add it by hand: Settings > Connectors > Add custom connector, then paste:

```
https://mcp.flystopover.com/mcp
```

### Claude Code

```bash
claude mcp add --transport http stopover https://mcp.flystopover.com/mcp
```

### ChatGPT

Turn on developer mode (Settings > Apps & Connectors > Advanced settings > Developer mode), then create a custom connector with:

- Name: Stopover
- MCP server URL: `https://mcp.flystopover.com/mcp`
- Authentication: No authentication

### Cursor

Add this to `~/.cursor/mcp.json` (or `.cursor/mcp.json` in a project):

```json
{
  "mcpServers": {
    "stopover": {
      "url": "https://mcp.flystopover.com/mcp"
    }
  }
}
```

### VS Code

Add this to `.vscode/mcp.json` in your workspace:

```json
{
  "servers": {
    "stopover": {
      "type": "http",
      "url": "https://mcp.flystopover.com/mcp"
    }
  }
}
```

### Windsurf and other clients

Most clients that support remote MCP servers take a block like this:

```json
{
  "mcpServers": {
    "stopover": {
      "serverUrl": "https://mcp.flystopover.com/mcp"
    }
  }
}
```

Windsurf uses `serverUrl`. Other clients may call the field `url`. If your client only supports local (stdio) servers, you can bridge with `mcp-remote`:

```json
{
  "mcpServers": {
    "stopover": {
      "command": "npx",
      "args": ["-y", "mcp-remote", "https://mcp.flystopover.com/mcp"]
    }
  }
}
```

## Good to know

- Prices come from free fare sources and are estimates at the time shown.
- Booking happens on the airline or booking site, never through Stopover.
- `server.json` in this repo is the same entry that is published to the official MCP Registry.

## Links

- Website: [flystopover.com](https://flystopover.com)
- Privacy: [flystopover.com/privacy](https://flystopover.com/privacy)
- Terms: [flystopover.com/terms](https://flystopover.com/terms)
- Support: [flystopover.com/support](https://flystopover.com/support)

## License

The docs in this repo are MIT licensed. See [LICENSE](LICENSE). The Stopover service itself is covered by its [terms](https://flystopover.com/terms).
