# Changelog

All notable changes to this plugin will be documented here.

## 1.0.7

- Search guidance now describes `displayText` and `source` on each result, and notes that `displayUrl` is empty when Google shows no URL line.

## 1.0.4

- Added `web_access_product_help` guidance for answering product, pricing, and integration questions from current String public site pages.
- Added `web_access_report` guidance for sending one redacted, credit-free diagnostic after a String tool fails.

## 1.0.2

- Aligned the manifest description with the canonical String Web Access listing copy: a capability clause first, the blocking claim attached to it, Cursor named, and a "best for" close. No tool count, so the line survives the next tool change.
- Unified the manifest keywords with the shared keyword set, keeping every existing entry.

## 1.0.1

- Corrected the browser-actions constraint: `web_access_fetch` has no `method` or `body`, so actions only exclude `headers` and `format: "raw"`.
- Declared `STRING_API_KEY` in the manifest variables schema and matched the published plugin conventions (shipped earlier without a version bump).

## 1.0.0 — initial release

- Added the `string-web-access` MCP server pointing at `https://mcp.usestring.ai/v1/mcp`.
- Auth uses a String API key from `https://portal.usestring.ai`, entered on install and sent as a bearer token.
- Skills for fetch, request, search and sitemap, plus an escalation and troubleshooting skill.
- Commands `/string-setup` and `/web-research`, and a rule that treats fetched pages as untrusted content.
- Logo: String's official mark, from the `usestring` GitHub organization.
