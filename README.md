# Inxy.ai SEO Audit — MCP Server

[![Inxy](https://img.shields.io/badge/by-inxy.ai-6366f1)](https://inxy.ai)

A remote [Model Context Protocol](https://modelcontextprotocol.io) server that lets any AI agent — Claude, ChatGPT, Cursor, and others — audit a website or Shopify store for **AEO / GEO / LLMO readiness**: how likely ChatGPT, Claude, Perplexity, and Google AI are to cite it.

- **Endpoint:** `https://inxy.ai/api/mcp` (Streamable HTTP)
- **Docs / setup:** https://inxy.ai/mcp
- **Tool:** `audit_seo(url)`

## What `audit_seo` does

Given a URL, it returns a **0–100 AI-readiness score** plus the top issues to fix:

- 12 universal AEO/GEO/LLMO checks (FAQ/structured-data/headings/llms.txt/meta/title/canonical/author/content depth/viewport/OG/citable stats).
- **Shopify deep-dive** — when a Shopify store is detected, 5 extra store-specific checks (Product / Offer / Review / Breadcrumb schema + product image alt coverage).
- A link to the full 12-category report + an automated 30-day fix plan at [inxy.ai](https://inxy.ai/free-seo-audit).

## Connect it

### Claude Desktop / Cursor / any MCP client

```json
{
  "mcpServers": {
    "inxy-seo": {
      "url": "https://inxy.ai/api/mcp"
    }
  }
}
```

### With an API key (10 audits/day + full detailed breakdown)

Generate a free key in your [Inxy account → Settings](https://app.inxy.ai/app/settings):

```json
{
  "mcpServers": {
    "inxy-seo": {
      "url": "https://inxy.ai/api/mcp",
      "headers": { "Authorization": "Bearer inxy_sk_YOUR_KEY" }
    }
  }
}
```

## Limits

| Tier | Limit | Report |
| --- | --- | --- |
| Anonymous | 5 audits / day | Score + top issues |
| API key (free) | 10 audits / day | Full detailed breakdown |
| Connected Shopify store | Higher | Full 12-category audit + automated 30-day fix plan |

## Example (raw JSON-RPC)

```bash
curl -s https://inxy.ai/api/mcp \
  -H 'Content-Type: application/json' \
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"audit_seo","arguments":{"url":"https://example.com"}}}'
```

## About Inxy.ai

[Inxy.ai](https://inxy.ai) is the autonomous AEO/SEO engine for Shopify stores — it doesn't just score your store, it auto-applies every fix and attributes the resulting revenue back to AI search.

---

_This repo holds the public MCP manifest (`server.json`) for registry discovery (modelcontextprotocol registry, Smithery, Glama, PulseMCP, mcp.so). The server itself is hosted by Inxy at the endpoint above._
