# Installing the MexCheck MCP server

MexCheck is a **remote** MCP server (Streamable HTTP). There is nothing to download, build or run locally, and no API key to paste.

## Steps

1. Add this entry to the MCP settings file of the client (for Cline: `cline_mcp_settings.json`):

```json
{
  "mcpServers": {
    "mexcheck": {
      "type": "streamableHttp",
      "url": "https://mexcheck.com/mcp"
    }
  }
}
```

   If the client only supports stdio servers, use the `mcp-remote` bridge instead:

```json
{
  "mcpServers": {
    "mexcheck": {
      "command": "npx",
      "args": ["-y", "mcp-remote", "https://mexcheck.com/mcp"]
    }
  }
}
```

2. Reload the MCP servers. `tools/list` and the docs tools (`list_docs`, `read_doc`, `get_openapi_operation`) work right away without signing in.
3. The first time a lookup tool is called (for example `rfc_validate` or `curp_lookup`), the server asks for OAuth 2.1 sign-in. The client opens a browser window; the user signs in or creates a MexCheck account (new accounts get a $5 USD credit bonus).

## Check it works

```sh
curl -s https://mexcheck.com/mcp \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json, text/event-stream' \
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/list"}'
```

Docs: https://mexcheck.com/docs/mcp
