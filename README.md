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
| MCP server | `mcp.json` (Agent Plugins), `.mcp.json` (host-specific manifests) | The hosted Adlicio server, about 40 tools |
| Skill | `skills/adlicio-get-started/SKILL.md` | First run: account, credits and a first task |
| Skill | `skills/adlicio-customer-research/SKILL.md` | How to run a research pass and report it |
| Skill | `skills/adlicio-ad-angles/SKILL.md` | Ad angles, hooks and scripts that quote real customers |
| Skill | `skills/adlicio-competitor-ads/SKILL.md` | Competitor ads, scripts and landing pages from the Meta Ad Library |
| Skill | `skills/adlicio-advertorial/SKILL.md` | Static image ads that send people to an article that sells, built from customer quotes and competitor advertorials |
| Skill | `skills/adlicio-forum-answers/SKILL.md` | Forum threads that rank on Google for your questions, with honest draft answers |
| Skill | `skills/adlicio-video-plan/SKILL.md` | For creators: what to film next, from what the audience asks, for one video or a week |
| Skill | `skills/adlicio-repurpose-video/SKILL.md` | For creators: Shorts with timestamps, X posts and community posts from one video's transcript |
| Skill | `skills/adlicio-viewer-questions/SKILL.md` | For creators: questions, reply drafts and spam to delete, from the comments under your own videos |

The three creator skills read a channel profile from `references/channel-profile.md`. It ships blank; the skill fills it in from the creator's channel on the first run and shows it back to keep.

## The MCP server

```
https://mcp.tryadlicio.com/mcp
```

Transport is streamable HTTP. Auth is OAuth 2.1 with dynamic client
registration, so the host needs no API key and no environment variables. The
first call opens a browser sign-in for the user's Adlicio account.

## What this plugin runs, sends and fetches

- **Runs:** nothing on your machine. The package is Markdown and JSON only: no
  local executable, hooks, commands, agents or install scripts.
- **Sends:** the tool arguments Claude passes (for example a keyword or a page
  URL) to `https://mcp.tryadlicio.com/mcp`, with your Adlicio sign-in token.
  It does not send your conversation.
- **Sign-in:** a browser OAuth sign-in to your Adlicio account at
  `tryadlicio.com`, with Google sign-in if you choose it.
- **Fetches:** the results of each tool call from the Adlicio server. The
  hosted service retrieves the public pages you ask for, and may use
  collection providers to do so.
- **Stores:** results go to your Adlicio history. Tools that create brands,
  save scripts or evidence, track sources or start background reports change
  your Adlicio workspace. No tool deletes data or posts to the sites it reads.

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

### Claude (claude.ai, desktop, Cowork and Claude Code)

Once the listing is live, add **Adlicio** from the Claude directory. On
claude.ai and in Cowork, open the plugin's **Connectors** tab, connect Adlicio
and sign in. Claude Code connects to the server when the plugin loads.

To install from this repository in Claude Code:

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

The server's tool list can change. Claude shows the current list when you
connect.

Scraping and search: `scrape_url`, `search_reddit`, `search_youtube`,
`search_blind`, `search_hackernews`, `research_topic`, `get_video_transcript`,
`start_deep_scrape`, `get_deep_scrape`.

Ad and creator research: `find_scroll_stoppers`, `find_creators`,
`find_competitor_brands`, `find_competitor_ads`, `find_tv_ads`,
`get_ad_transcript`, `inspect_landing_page`, `find_products`,
`find_early_products`, `get_linkedin_profile`.

Reports: `start_brand_research`, `get_brand_research`, `start_voc_report`,
`get_voc_report`, `get_audience`.

Listening and Radar: `add_tracked_source`, `list_tracked_sources`,
`create_radar`, `update_radar`, `check_radar`, `list_radar_posts`,
`set_radar_post_status`.

Workspace and history: `create_brand`, `save_script`, `save_evidence`,
`list_history`, `search_history`, `get_history_item`, `scrape_facebook_group`,
`get_extension_job`, `whoami`.

`scrape_url` supports Amazon, Trustpilot, G2, Etsy, Walmart, eBay, Sephora,
Ulta, AliExpress, TripAdvisor, Better Business Bureau, Google Maps, Reviews.io,
Shopify and DTC product pages with Yotpo, Loox or Judge.me, the Apple App
Store, Google Play, Steam, YouTube, TikTok, Instagram posts and reels, public
Facebook posts, public LinkedIn posts, X posts, Reddit threads and profiles,
Hacker News, Product Hunt, Quora, Stack Exchange, Blind, forum threads
(Discourse, XenForo, vBulletin, phpBB, Invision), Disqus comments and Notion
pages.

## Access and credits

Connect with your own Adlicio account. Full platform access requires All Access;
other accounts may connect but have limited tool access. Check `whoami` for the
connected account's access and research balance. The open-source plugin package
is free; the hosted service has account and credit requirements.

`whoami` and reading stored history cost 0 research credits. `scrape_url`
costs 0 on direct sources such as YouTube, app stores, Steam and Shopify pages
and usually 1 credit on paid collection sources. Other research tools state
their own cost. Read each tool's current
description before starting metered work, and keep usage within the user's
request. A plan or credit error must be reported rather than retried in a loop.
Facebook group collection requires the user's configured Adlicio Chrome
extension and their existing access to the group.

## Privacy, terms, and support

- [Privacy policy](https://tryadlicio.com/privacy)
- [Service terms](https://tryadlicio.com/terms)
- Support: team@tryadlicio.com
- The MIT license applies to this plugin package. Use of the hosted Adlicio
  service is governed by Adlicio's service terms.

## Related

- Setup and plans: <https://tryadlicio.com/mcp>
- CLI and MCP docs: <https://github.com/daniel-ddtech/commentscraper-cli>
- npm CLI: `npm install -g commentscraper`
- MCP Registry entry: `com.tryadlicio/adlicio`

## License

MIT. See [LICENSE](LICENSE).

Contact: team@tryadlicio.com
