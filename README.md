# MyTelescope Orchestrator MCP Server

A hosted Model Context Protocol (MCP) server from [MyTelescope](https://mytelescope.io).

> TODO: one-paragraph description of what this server exposes — tools, resources, typical use cases.

## Connection

- **Endpoint:** `https://mytelescope-orchestrator-mcp-amjjfcdvoa-uc.a.run.app/mcp`
- **Transport:** Streamable HTTP
- **Auth:** TODO — describe whether an API key / bearer token is required, and how to obtain one.

## Client setup

### Claude Desktop / Claude Code

Add to your MCP client config:

```json
{
  "mcpServers": {
    "mytelescope-orchestrator": {
      "url": "https://mytelescope-orchestrator-mcp-amjjfcdvoa-uc.a.run.app/mcp",
      "transport": "streamable-http"
    }
  }
}
```

If auth is required, add the appropriate header (e.g., `Authorization: Bearer <token>`).

### Cursor / other MCP clients

Point the client at the endpoint above using the streamable-HTTP transport.

## Registry

This server is listed on the [official MCP Registry](https://registry.modelcontextprotocol.io/) under the namespace `io.github.mytelescope/orchestrator`.

## Support

- Issues: open a GitHub issue on this repo
- Contact: theesh@mytelescope.io

## License

MIT — see [LICENSE](./LICENSE).
