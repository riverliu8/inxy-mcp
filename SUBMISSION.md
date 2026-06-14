# Submitting the Inxy MCP server to directories

Reusable metadata for every directory:

| Field | Value |
| --- | --- |
| Name (id) | `inxy-seo` |
| Display name | `Inxy SEO Audit` |
| Namespace (official registry) | `ai.inxy/seo-audit` |
| Server endpoint | `https://inxy.ai/api/mcp` |
| Transport | Streamable HTTP |
| Tool | `audit_seo(url)` |
| One-liner | Score any website or Shopify store for AEO/GEO/LLMO readiness — how likely ChatGPT, Claude, Perplexity & Google AI are to cite it. Shopify stores get a deeper report. |
| Category / tags | SEO, Marketing, Shopify, AEO, web |
| Website / docs | `https://inxy.ai/mcp` |
| Manifest | `https://inxy.ai/.well-known/mcp/server.json` |
| Repo | `https://github.com/<YOUR_ORG>/inxy-mcp` |
| Auth | Optional `Authorization: Bearer inxy_sk_…` (free key in app Settings) |

---

## 1. Official registry (registry.modelcontextprotocol.io)

This is the highest-value listing. Publishing is done with the `mcp-publisher` CLI, not a web form.

**Pick a namespace first** — two options:

- **`io.github.<YOUR_ORG>/inxy-seo`** — easiest. Ownership is proven by logging in with the GitHub account/org that owns the repo. No DNS needed.
- **`ai.inxy/seo-audit`** — branded (what `server.json` currently uses). Requires proving you own `inxy.ai` via a **DNS TXT record**.

**Steps (GitHub namespace — recommended to start):**
```bash
# 1. install the publisher
brew install mcp-publisher   # or: go install github.com/modelcontextprotocol/registry/cmd/mcp-publisher@latest

# 2. authenticate with the GitHub org that owns the repo
mcp-publisher login github

# 3. from mcp-server/ (with server.json), set name to io.github.<ORG>/inxy-seo, then:
mcp-publisher publish
```

**Steps (domain namespace `ai.inxy` — branded):**
```bash
mcp-publisher login dns --domain inxy.ai
```
The CLI prints the **exact DNS TXT record to add** (a `_mcp.inxy.ai` TXT record containing a tool-generated key/challenge — do NOT invent the value, use what the CLI outputs). Add it at the Cloudflare DNS dashboard for inxy.ai, wait for propagation, re-run the login, then `mcp-publisher publish`.

> Keep `server.json`'s `name` consistent with the namespace you chose before publishing.

---

## 2. Smithery (smithery.ai)

Easiest path: connect the public GitHub repo (`inxy-mcp`) — Smithery auto-detects `server.json`.
- "Add Server" → connect GitHub → select the repo.
- Type: **Remote / hosted** (HTTP). Endpoint: `https://inxy.ai/api/mcp`.
- Fill display name, description, tags from the table above.

## 3. Glama (glama.ai/mcp/servers)

Form-based ("Add MCP Server"):
- Name: `Inxy SEO Audit` · Repo URL: the GitHub repo · Type: Remote (HTTP).
- Endpoint `https://inxy.ai/api/mcp` · description + tags from the table.

## 4. PulseMCP (pulsemcp.com)

"Submit a server":
- Name / one-liner / category from the table · Type: Remote · URL `https://inxy.ai/api/mcp` · Docs `https://inxy.ai/mcp`.

## 5. mcp.so

"Submit" → repo URL + the metadata above.

---

## After listing

- Verify each listing's "connect" config points at `https://inxy.ai/api/mcp`.
- Spot-check the live server anytime: `node tests/e2e/mcp-e2e.mjs`.
