# MexCheck MCP server

Remote [Model Context Protocol](https://modelcontextprotocol.io) server for **Mexican identity and tax checks**, answered by the registries that own the data: SAT, RENAPO, INE and CFE.

- **Endpoint:** `https://mexcheck.com/mcp` (Streamable HTTP)
- **Auth:** OAuth 2.1 (dynamic client registration + PKCE). No API key to paste; your client opens a browser to sign in. `tools/list` and the docs tools work before login.
- **Docs:** https://mexcheck.com/docs/mcp
- **Official MCP Registry:** `com.mexcheck/mexcheck`

This repository holds documentation and client configuration only. The server is hosted by MexCheck; its source is not public.

## What it can do

| Tool | What it does |
| --- | --- |
| `rfc_validate` | Full RFC validation with SAT (certificate lookup, zip search, lists) |
| `rfc_verify` | Verify an RFC, optionally against a name + zip |
| `rfc_profile` | Registered taxpayer data for an RFC |
| `rfc_find_zip` | SAT-registered zip code for a known RFC + name |
| `rfc_sat_lists` | SAT 69 / 69-B / 69-B Bis lists an RFC appears in |
| `cfdi_verify` | CFDI (invoice) status with SAT |
| `csf_verify` | Read and verify a Constancia de Situación Fiscal |
| `curp_lookup` | Look up a CURP in RENAPO |
| `curp_search` | Find a CURP by personal data |
| `ine_verify` | INE voter ID status |
| `cfe_verify` | Verify a CFE electricity receipt |
| `geo_zip`, `geo_zip_search` | Mexican zip code lookup and search |
| `list_docs`, `read_doc`, `get_openapi_operation` | REST API docs and OpenAPI 3.1 operations (free, no login) so a coding assistant can write the integration |
| `get_account`, `create_api_key`, `list_plans`, `create_plan_checkout`, `create_balance_checkout`, `charge_saved_card`, `get_billing_portal_link` | Account, API keys and billing |

Lookups call the real government registries and are billed to the connected account in credits.

## Pricing

One credit balance for every product: pay as you go at **$0.015 USD per credit** with a **$5 USD signup bonus**, or plans from **$99 USD/month**. Requests that produce no answer (upstream outage, our error) are not charged. See https://mexcheck.com/pricing.

## Connect

### Claude Code

```sh
claude mcp add --transport http mexcheck https://mexcheck.com/mcp
```

### Claude Desktop / Claude.ai

Settings → Connectors → Add custom connector → URL `https://mexcheck.com/mcp`.

### Cursor (`~/.cursor/mcp.json`)

```json
{
  "mcpServers": {
    "mexcheck": { "url": "https://mexcheck.com/mcp" }
  }
}
```

### VS Code (`.vscode/mcp.json`)

```json
{
  "servers": {
    "mexcheck": { "type": "http", "url": "https://mexcheck.com/mcp" }
  }
}
```

### Clients without remote/OAuth support (via `mcp-remote`)

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

More examples in [`examples/`](examples/).

## REST API

Prefer plain HTTP? The same checks are available as a REST API with API keys: https://mexcheck.com/docs (OpenAPI: https://mexcheck.com/openapi.json).

## Support

adrian@mexcheck.com · https://mexcheck.com

## License

Documentation and examples in this repository: MIT. The MexCheck service has its own terms at https://mexcheck.com.
