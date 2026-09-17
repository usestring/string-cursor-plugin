# String Web Access

Cursor plugin that connects agents to [String Web Access](https://usestring.ai) through String's
hosted remote [Model Context Protocol](https://modelcontextprotocol.io/) server.

Web search, content extraction, and site mapping, returned as clean Markdown from any site —
including the ones that block bots.

## Install

1. Open **Cursor Settings → Plugins**.
2. Search for **String Web Access**.
3. Click **Install**, then paste a String API key when prompted.

Or run `/add-plugin string-web-access` in chat.

Keys come from [portal.usestring.ai](https://portal.usestring.ai).

## MCP

```json
{
  "mcpServers": {
    "string-web-access": {
      "type": "http",
      "url": "https://mcp.usestring.ai/v1/mcp",
      "headers": { "Authorization": "Bearer ${STRING_API_KEY}" }
    }
  }
}
```

The key is stored as the plugin variable `STRING_API_KEY` and sent as a bearer token. The server
also advertises OAuth 2.1 protected-resource metadata, so a client that prefers sign-in over a key
can use that instead.

## What agents can do

| Tool | Capability |
| --- | --- |
| `web_access_fetch` | Fetch one URL as Markdown, with optional browser actions and JSON or raw output |
| `web_access_request` | Send a POST, PUT or PATCH with a body to a URL |
| `web_access_search` | Search the web and get structured results back |
| `web_access_sitemap` | Crawl a site and map its URLs as an asynchronous, quoted job |
| `web_access_report` | Send one redacted, credit-free failure diagnostic to String support |

The hosted runtime is the source of truth for tool names and schemas.

## What's in the plugin

| Component | Contents |
| --- | --- |
| Skills | `string-web-access` (escalation and troubleshooting), plus `string-fetch`, `string-request`, `string-search`, `string-sitemap`, `string-report` |
| References | Browser actions, response formats, query construction |
| Commands | `/string-setup`, `/web-research` |
| Rules | Handling fetched web content as untrusted data |
| MCP | Hosted server at `https://mcp.usestring.ai/v1/mcp` (streamable HTTP) |

## Notes

- `web_access_fetch` and `web_access_search` are read-only.
- `web_access_request` writes, and `web_access_sitemap` creates billed crawl jobs, so both prompt
  before they run.
- A sitemap crawl is quoted before it bills: nothing is fetched until the quote is approved.
- After every failed String call, `web_access_report` sends one credential-free diagnostic before
  any retry or fallback, even when recovery later succeeds. Expected negative results are not failures.

## Docs

- MCP overview: https://portal.usestring.ai/docs/mcp/overview
- Server URL: https://mcp.usestring.ai/v1/mcp

Logo is String's official mark, from the `usestring` GitHub organization.

## License

MIT
