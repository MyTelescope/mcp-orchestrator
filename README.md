# MyTelescope Orchestrator MCP Server

A hosted Model Context Protocol (MCP) server from [MyTelescope](https://mytelescope.io).

## What is MyTelescope?

MyTelescope is a demand intelligence platform for marketers and growth teams. It turns real-world search and behavioral signals into decisions — which keywords are rising, which markets are heating up, which competitors are gaining share, and where to place the next bet.

Core capabilities exposed through this MCP server include:

- **Demand signals** — track how demand for a topic, product, or category evolves over time and geography.
- **Priorities & share** — calculate relative demand share between competitors, brands, or keywords.
- **Trajectory & forecasting** — project where demand is heading (short-term and seasonal).
- **Emerging demand** — surface fast-growing topics before they become obvious.
- **Signal collections** — query curated, private, or public collections of market signals.
- **Location intelligence** — scope any analysis to a country, region, or city.

By connecting MyTelescope to an MCP-compatible client (Claude Desktop, Claude Code, Cursor, etc.), you can ask questions like "is demand for X rising in Germany?" or "who's gaining share in the running-shoe category this quarter?" and get grounded, data-backed answers inside your normal workflow.

## Authentication

The server uses **OAuth 2.1 with PKCE** backed by Firebase. You do **not** need to paste an API key — your MCP client handles the flow automatically.

**What happens when you connect:**

1. Your MCP client connects to the server and receives a `401` challenge.
2. The client opens MyTelescope's hosted login page in your browser.
3. You sign in with your MyTelescope account (email/password or Google).
4. The browser redirects back to your client, which receives and stores an access token.
5. All subsequent MCP calls include the token automatically.

**To use MyTelescope through MCP you need a MyTelescope account.** If you don't have one, sign up at [mytelescope.io](https://mytelescope.io). Tool calls are metered against your account's credit balance, the same way they are inside the MyTelescope web app.

## Client setup

MCP clients fall into two groups:

- **Native remote support** — the client speaks streamable-HTTP directly.
- **Stdio-only** — the client only launches local processes; use `npx mcp-remote` as a bridge.

Both paths trigger the same browser-based login on first use.

### Option A — native remote (Claude Code, Cursor, recent Claude Desktop)

Claude Code CLI:

```bash
claude mcp add --transport http mytelescope \
  https://mytelescope-orchestrator-mcp-amjjfcdvoa-uc.a.run.app/mcp
```

Claude Desktop / Cursor config:

```json
{
  "mcpServers": {
    "mytelescope": {
      "url": "https://mytelescope-orchestrator-mcp-amjjfcdvoa-uc.a.run.app/mcp",
      "transport": "streamable-http"
    }
  }
}
```

### Option B — stdio bridge via `npx mcp-remote`

For clients that don't yet support remote transport natively, use [`mcp-remote`](https://www.npmjs.com/package/mcp-remote). It's an npm package run on the fly with `npx` — no install step, and it handles OAuth + token caching for you. Requires Node.js 18+.

```json
{
  "mcpServers": {
    "mytelescope": {
      "command": "npx",
      "args": [
        "-y",
        "mcp-remote",
        "https://mytelescope-orchestrator-mcp-amjjfcdvoa-uc.a.run.app/mcp"
      ]
    }
  }
}
```

On first launch, `mcp-remote` opens your browser for the MyTelescope login, then caches the token under `~/.mcp-auth/` so future launches are silent until the token expires.

## Registry

This server is listed on the [official MCP Registry](https://registry.modelcontextprotocol.io/) under the namespace `io.github.mytelescope/orchestrator`.

## Support

- Issues: open a GitHub issue on this repo
- Contact: theesh@mytelescope.io

## License and terms of use

**The MIT license in this repository covers only the contents of this repository** — the README, the `server.json` manifest, and example snippets. You are free to copy, fork, or adapt those files.

**The MyTelescope service is a paid SaaS product and is not free.** The MIT license does **not** grant any right to use, access, or redistribute:

- The MyTelescope orchestrator service or any hosted MCP endpoint operated by MyTelescope
- MyTelescope's APIs, demand signals, forecasts, or any data served through them
- The MyTelescope brand, trademarks, or logos

Use of the MyTelescope service requires a MyTelescope account and is governed by the [MyTelescope Terms of Service](https://mytelescope.io/terms) and [Privacy Policy](https://mytelescope.io/privacy). Tool calls made through this MCP server consume credits from your MyTelescope account.

See [LICENSE](./LICENSE) for the full MIT text applied to this repository.
