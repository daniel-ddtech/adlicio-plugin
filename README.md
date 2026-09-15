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
| MCP server | `mcp.json` (Agent Plugins), `.mcp.json` (host-specific manifests) | The hosted Adlicio server, 30 tools |
| Skill | `skills/adlicio-customer-research/SKILL.md` | How to run a research pass and report it |

## The MCP server

```
https://mcp.tryadlicio.com/mcp
```

Transport is streamable HTTP. Auth is OAuth 2.1 with dynamic client
registration, so the host needs no API key and no environment variables. The
first call opens a browser sign-in for the user's Adlicio account.

Tool requests go to `mcp.tryadlicio.com`. Browser authentication also uses
Adlicio's sign-in services and, if selected, Google sign-in. This package has no
local executable, hooks, or install scripts. Requests and results are processed
by Adlicio and the connected host; the hosted service may use collection
providers to retrieve the requested sources.

## Install

### Cursor and Grok Bot

This package is prepared for marketplace review. It is not yet a published
Cursor Marketplace listing. Once approved, search for **Adlicio** in the
marketplace, add it, and complete Adlicio's browser authorization when prompted.

For local testing in Cursor, clone this repository into
`~/.cursor/plugins/local/adlicio`, reload Cursor, and check Customize for the
`adlicio` MCP server and `adlicio-customer-research` skill. Local plugin imports
must be allowed by your team. Grok Bot's in-app marketplace installation remains
subject to review and availability.

Try these prompts after connecting:

- "Use Adlicio to check my account access and remaining research credits."
- "Use Adlicio to find three Reddit discussions about choosing a CRM for a small business. Link each source."
- "Use my existing Adlicio research history to summarize customer objections."

The package includes a standard root `plugin.json` and `mcp.json`, plus a
`.cursor-plugin/plugin.json` that explicitly references `.mcp.json`.

### Claude Code

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
`find_competitor_ads`, `find_tv_ads`, `get_ad_transcript`, `inspect_landing_page`,
`find_products`, `find_early_products`, `save_script`.

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

Connect with your own Adlicio account. Full platform access requires All Access;
other accounts may connect but have limited tool access. Check `whoami` for the
connected account's access and research balance. The open-source plugin package
is free; the hosted service has account and credit requirements.

`search_reddit` costs 1 research credit; `search_youtube`, `whoami`, and reading
stored history cost 0. Collection costs depend on the source and collection
method. Other research tools have their own costs. Read each tool's current
description before starting metered work, and keep usage within the user's
request. A plan or credit error must be reported rather than retried in a loop.
Facebook group collection requires the user's configured Adlicio Chrome
extension and their existing access to the group.

## Privacy, terms, and support

- [Privacy policy](https://tryadlicio.com/privacy)
- [Service terms](https://tryadlicio.com/terms)
- Support: daniel@tryadlicio.com
- The MIT license applies to this plugin package. Use of the hosted Adlicio
  service is governed by Adlicio's service terms.

## Related

- Setup and plans: <https://tryadlicio.com/mcp>
- CLI and MCP docs: <https://github.com/daniel-ddtech/commentscraper-cli>
- npm CLI: `npm install -g commentscraper`
- MCP Registry entry: `com.tryadlicio/adlicio`

## License

MIT. See [LICENSE](LICENSE).

Contact: daniel@tryadlicio.com
