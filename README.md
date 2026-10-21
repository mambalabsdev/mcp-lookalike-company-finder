# Lookalike Company Finder MCP Server

[![Smithery](https://smithery.ai/badge/mambabuilt/mcp-lookalike-company-finder)](https://smithery.ai/servers/mambabuilt/mcp-lookalike-company-finder) [![Glama score](https://glama.ai/mcp/servers/mambalabsdev/mcp-lookalike-company-finder/badges/score.svg)](https://glama.ai/mcp/servers/mambalabsdev/mcp-lookalike-company-finder) [![MCP Registry](https://img.shields.io/badge/dynamic/json?url=https%3A%2F%2Fregistry.modelcontextprotocol.io%2Fv0%2Fservers%3Fsearch%3Dcom.mambabuilt%252Fmcp-lookalike-company-finder%26limit%3D1&query=%24.servers%5B0%5D._meta%5B%22io.modelcontextprotocol.registry%2Fofficial%22%5D.status&label=mcp%20registry&color=blue)](https://registry.modelcontextprotocol.io/v0/servers?search=com.mambabuilt/mcp-lookalike-company-finder&limit=1) [![npm version](https://img.shields.io/npm/v/@mambalabsdev/mcp-lookalike-company-finder)](https://www.npmjs.com/package/@mambalabsdev/mcp-lookalike-company-finder) [![npm downloads](https://img.shields.io/npm/dm/@mambalabsdev/mcp-lookalike-company-finder)](https://www.npmjs.com/package/@mambalabsdev/mcp-lookalike-company-finder) [![license](https://img.shields.io/github/license/mambalabsdev/mcp-lookalike-company-finder)](https://github.com/mambalabsdev/mcp-lookalike-company-finder/blob/main/LICENSE) [![mcpservers.org](https://img.shields.io/badge/mcpservers.org-listed-blue)](https://mcpservers.org/servers/mambalabsdev/mcp-lookalike-company-finder)

An MCP server for the Mamba Labs Lookalike Company Finder actor on Apify. Give it seed company domains. Each run returns similar companies ranked by a similarity score, with the evidence behind each score.

## What's Inside

- [What it does](#what-it-does)
- [Quick start](#quick-start)
- [Prerequisites](#prerequisites)
- [Example prompts](#example-prompts)
- [Tool](#tool)
- [Inputs](#inputs)
- [Pricing](#pricing)
- [Your keys](#your-keys)
- [Full actor documentation](#full-actor-documentation)
- [License](#license)

## What it does

Candidates come from the seed's "alternatives", "vs", and "competitors" search result pages and from the products list articles name, matched to their own sites. Each candidate homepage is read and compared with the seeds: shared distinctive words, search mentions, whether a comparison names it, and shared tools. Optional checks start Mamba Labs actors as child runs: Website Phrase and Business Model Classifier (on by default), B2B Reddit Conversation Monitor, and Integration and Marketplace Presence Mapper; Apify bills each to your account at its own prices. Review sites, list articles, and media are never returned.

All of the work runs on Apify. This package is a thin client that starts the actor run, waits for it, and hands back the dataset rows.

## Quick start

You need Node.js 18 or newer and an Apify account with an API token.

Add this to your Claude Desktop config (`claude_desktop_config.json`), Cursor, or any MCP client:

```json
{
  "mcpServers": {
    "mamba-lookalike-company-finder": {
      "command": "npx",
      "args": [
        "-y",
        "@mambalabsdev/mcp-lookalike-company-finder"
      ],
      "env": {
        "APIFY_TOKEN": "your-apify-token"
      }
    }
  }
}
```

Restart the client. The `find_lookalike_companies` tool appears.

## Prerequisites

- Node.js 18 or newer.
- An Apify API token from [console.apify.com/account/integrations](https://console.apify.com/account/integrations), set as `APIFY_TOKEN`. The server lists its tool without a token; a call needs one.

## Example prompts

- "Find 25 companies similar to smartlead.ai and instantly.ai, best match first."
- "Which companies look like gong.io? Show why each one ranks where it does."
- "Build a lookalike list from my three best customers, excluding mycompany.com."

## Tool

`find_lookalike_companies`. One tool. Example arguments:

```json
{
  "seed_domains": [
    "smartlead.ai"
  ],
  "max_results": "25"
}
```

## Inputs

Every buyer facing input of the actor, unchanged. Omitted inputs take the actor's own defaults. Numbers and booleans are sent as strings.

| Input | Type | Description |
|---|---|---|
| `seed_domains` | array | One to ten seed company domains |
| `seed_domain` | string | One seed domain |
| `max_results` | string | 1 to 100. Default 25 |
| `min_score` | string | 0 to 100. Default 20 |
| `use_classifier` | string | Business model check, child run. Default true |
| `classify_top_n` | string | 1 to 50. Default 15 |
| `use_reddit` | string | Reddit co-mentions, child run. Default false |
| `use_marketplaces` | string | Marketplace overlap, child run. Default false |
| `exclude_domains` | array | Domains never to return |
| `max_charge_usd` | string | Optional cost cap for the run |

## Pricing

Pay per event on Apify, billed to your Apify account. Prices in USD.

| Event | Free plan | Bronze | Silver | Gold |
|---|---|---|---|---|
| `lookalike-company`, per company returned | $0.005 | $0.00475 | $0.0045 | $0.00425 |
| `apify-actor-start`, per run start | $0.0005 | $0.0005 | $0.0005 | $0.0005 |

The seed summary row, no results rows, and error rows are free. The optional checks start Mamba Labs actors from your Apify account, billed at their own prices: Website Phrase and Business Model Classifier per domain classified, B2B Reddit Conversation Monitor per thread and summary row, Integration and Marketplace Presence Mapper per listing found.

## Your keys

The actor needs no key. It reads search result pages and company homepages through the Apify proxy and holds no key of any kind. Mamba Labs pays the platform and proxy costs of this actor's own run; child runs are billed by their own actors.

## Full actor documentation

[apify.com/mambalabs/lookalike-company-finder](https://apify.com/mambalabs/lookalike-company-finder)

## License

MIT. See [LICENSE](LICENSE).
