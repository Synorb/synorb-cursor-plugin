# Synorb for Cursor and Grok Bot

Cursor plugin that connects your agent to [Synorb](https://synorb.com)'s hosted [Model Context Protocol](https://modelcontextprotocol.io/) server.

Synorb turns thousands of sources into Streams of source-cited Manifests. With this plugin your agent can search Streams, pull Manifests with their source URLs, and save Beacons that it pulls again later.

## Install

1. Open **Plugins** in Cursor or Grok Bot.
2. Search for **Synorb**.
3. Click **Install**, then complete the Synorb sign-in.

Or run `/add-plugin synorb` in chat.

Sign-in uses OAuth. A new email gets a free Synorb account. There is no key or token to paste, and the plugin never asks for one.

## MCP

```json
{
  "mcpServers": {
    "synorb": {
      "type": "http",
      "url": "https://mcp.synorb.com/mcp",
      "auth": {
        "CLIENT_ID": "synorb-cursor",
        "scopes": ["read:mcp", "read:beacons", "write:beacons"]
      }
    }
  }
}
```

`synorb-cursor` is a public OAuth client identifier. It uses PKCE and has no client secret. This repository holds no secret.

## Network endpoints and credentials

The plugin connects only to Synorb:

- `https://mcp.synorb.com/mcp` is the MCP server (Streamable HTTP).
- `https://api.synorb.com/oauth/authorize` and `https://api.synorb.com/oauth/token` are the sign-in endpoints. The metadata is at `https://api.synorb.com/.well-known/oauth-authorization-server`.

Scopes the plugin asks for:

| Scope | Why |
| --- | --- |
| `read:mcp` | Search Streams, read details and pull Manifests |
| `read:beacons` | List and draft Beacons |
| `write:beacons` | Save and archive a Beacon, only after you say yes |

## Tools

| Tool | Writes? | Use |
| --- | --- | --- |
| `synorb-profile` | No | Plan, usage and freshness |
| `synorb-stream-search` | No | Find Streams, sources and publishers |
| `synorb-catalog` | No | Rank Streams for a broad topic |
| `synorb-details` | No | Sources and filters of a Stream |
| `synorb-manifests` | No | Pull cited Manifests. Uses your Manifest allowance |
| `synorb-beacons` | No | List saved Beacons |
| `synorb-configure-beacon` | No | Draft a Beacon proposal |
| `synorb-save-beacon` | Yes | Save a Beacon, only after your explicit yes |
| `synorb-archive-beacon` | Yes | Archive a Beacon, only after your explicit yes |
| `synorb-get-demo-key` | Yes | Not used by this plugin. For sessions without sign-in |

## Skills

- `synorb-manifests` explains how to find Streams and pull cited Manifests with an explicit date window.
- `synorb-beacons` explains how to list, draft, save and run Beacons, and requires a clear yes before any write.

The hosted server is the source of truth for tool names and schemas.

## About this repository

This repository is the plugin: a manifest, an MCP entry and two skills. It contains no scripts and runs no code. It is not the MCP server, which is a hosted Synorb service.

## Links

- Homepage: https://synorb.com
- Agent documentation: https://synorb.com/agents
- Support: team@synorb.com
- Security: see [SECURITY.md](SECURITY.md)

## License

MIT. See [LICENSE](LICENSE).
