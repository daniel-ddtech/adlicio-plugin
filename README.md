<p align="center">
  <img src="assets/logo-400.png" width="96" alt="Adlicio" />
</p>

# Adlicio plugin

Agent plugin for [Adlicio](https://tryadlicio.com), a customer-voice research
tool for marketers and ad operators. It wires an agent to Adlicio's hosted MCP
server and adds a skill that tells the agent how to use it.

Adlicio gives agents real customer language. Scrape comments and reviews from
Reddit, YouTube, Amazon, TikTok, Instagram, Trustpilot, app stores and 20+ other
sources, search Reddit and YouTube, pull top-performing TikTok and Instagram
videos with their hooks, find competitor ads from the Meta Ad Library, and build
brand and voice-of-customer reports.

## What it ships

| Component | Path | What it is |
| --- | --- | --- |
| MCP server | `.mcp.json` | The hosted Adlicio server, about 27 tools |
| Skill | `skills/adlicio-customer-research/SKILL.md` | How to run a research pass and report it |

## The MCP server

```
https://mcp.tryadlicio.com/mcp
```

Transport is streamable HTTP. Auth is OAuth 2.1 with dynamic client
registration, so the host needs no API key and no environment variables. The
first call opens a browser sign-in for the user's Adlicio account.

Network endpoints called: `mcp.tryadlicio.com` only. No local shell, no
filesystem access, no hooks, no postinstall scripts.

## Install

Claude Code:

```bash
/plugin marketplace add daniel-ddtech/adlicio-plugin
/plugin install adlicio@adlicio
```

Any MCP client, without the plugin wrapper:

```bash
claude mcp add --transport http adlicio https://mcp.tryadlicio.com/mcp
```

Manual client config:

```json
{
  "mcpServers": {
    "adlicio": {
      "type": "http",
      "url": "https://mcp.tryadlicio.com/mcp"
    }
  }
}
```

Per-host setup pages, including Cursor, Lovable, Bolt, Replit, v0 and Base44,
are at <https://tryadlicio.com/mcp>.

## Tools

Scraping and search: `scrape_url`, `search_reddit`, `search_youtube`,
`search_blind`, `research_topic`, `start_deep_scrape`, `get_deep_scrape`.

Ad and creator research: `find_scroll_stoppers`, `find_creators`,
`find_competitor_ads`, `find_products`, `find_early_products`, `save_script`.

Reports: `start_brand_research`, `get_brand_research`, `start_voc_report`,
`get_voc_report`, `get_audience`.

Listening and history: `create_brand`, `add_tracked_source`,
`list_tracked_sources`, `list_history`, `search_history`, `get_history_item`,
`scrape_facebook_group`, `get_extension_job`, `whoami`.

`scrape_url` supports Reddit, YouTube, Amazon, the Apple App Store, Google Play,
Steam, Trustpilot, Reviews.io, Etsy, Walmart, Sephora, Ulta, eBay, Better
Business Bureau, G2, AliExpress, TripAdvisor, Stack Exchange, Discourse, phpBB,
XenForo, vBulletin, Invision Community, Hacker News, Quora, Product Hunt,
Shopify and DTC product pages including Yotpo and Loox, Disqus comments, public
Facebook posts, public LinkedIn posts, public Blind posts, public Instagram
posts and reels, TikTok videos, and Notion pages.

## Access and credits

The MCP server, the CLI and the web app need the Adlicio All Access plan. The
Pro plan covers the Chrome extension only. A free account can connect and see
the tools, but most tools spend research credits. `search_reddit` and
`search_youtube` cost no credits.

## Related

- Setup and plans: <https://tryadlicio.com/mcp>
- CLI and MCP docs: <https://github.com/daniel-ddtech/commentscraper-cli>
- npm CLI: `npm install -g commentscraper`
- MCP Registry entry: `com.tryadlicio/adlicio`

## License

MIT. See [LICENSE](LICENSE).

Contact: daniel@tryadlicio.com
