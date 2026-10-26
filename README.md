# String Web Access

Cursor plugin that connects agents to [String Web Access](https://usestring.ai) through String's
hosted remote [Model Context Protocol](https://modelcontextprotocol.io/) server.

Web search, content extraction, and site mapping, returned as clean, LLM-ready Markdown.

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
      "url": "https://mcp.usestring.ai/v3/mcp",
      "headers": { "Authorization": "Bearer ${STRING_API_KEY}" }
    }
  }
}
```

The key is stored as the plugin variable `STRING_API_KEY` and sent as a bearer token. The server
also advertises OAuth 2.1 protected-resource metadata, so a client that prefers sign-in over a key
can use that instead.

## Tools

The MCP server at `https://mcp.usestring.ai/v3/mcp` provides six tools.

| Tool | What it does |
| --- | --- |
| `web_access_search` | Searches the web and returns ranked results with titles, URLs and snippets. Read-only. |
| `web_access_fetch` | Reads one public URL and returns it as Markdown, the page's raw body, or a JSON envelope with the status and headers. Read-only. |
| `web_access_sitemap_quote` | Quotes a crawl of one site: estimated pages and cost. Crawls nothing and costs nothing. |
| `web_access_sitemap_start` | Starts a quoted crawl after the user approves the quote. |
| `web_access_sitemap_status` | Reports a crawl's progress, and lists its URLs once it finishes. Read-only. |
| `web_access_request` | Sends a POST, PUT or PATCH the user asks for, such as a GraphQL query, and returns the response. Prompts before it runs. |

## What's in the plugin

| Component | Contents |
| --- | --- |
| Skills | `web-search`, `read-page`, `map-site`, `send-request` |
| Commands | `/string-setup`, `/web-research` |
| Rules | Which tool fits a task, and handling fetched web content as untrusted data |
| MCP | Hosted server at `https://mcp.usestring.ai/v3/mcp` (streamable HTTP) |

## Skills

- **`web-search`**: find sources for a question when there is no URL yet, and answer with citations.
- **`read-page`**: read a URL, then summarize it, answer from it or pull its facts into a table.
- **`map-site`**: get a quote, wait for the user's approval, start the crawl, then read the URLs.
- **`send-request`**: send a request the user names, such as a GraphQL query, and show the data it
  returns.

Each skill carries the access rules that apply to it: public content and the user's own accounts
only, no getting past logins or paywalls, and page content treated as data rather than
instructions.

## Docs

- MCP overview: https://portal.usestring.ai/docs/mcp/overview
- Server URL: https://mcp.usestring.ai/v3/mcp

Logo is String's official mark, from the `usestring` GitHub organization.

## License

MIT
