---
name: adlicio-get-started
description: >-
  Introduce Adlicio and run a first research task. Use when the user has just
  connected Adlicio, asks what Adlicio can do or how to start, or asks about
  their Adlicio plan or research credits.
---

# Get started with Adlicio

Adlicio collects what customers say in public comments and reviews and returns
it as verbatim quotes with links to the source, for ad angles, hooks, landing
pages and positioning.

1. Call `whoami`. It costs 0 research credits. Tell the user their plan and
   their remaining research credits in one line.
2. Say in two or three sentences what Adlicio can do here: read the comments
   and reviews on over 30 platforms, search Reddit, YouTube, Blind and Hacker
   News for pages to read, look up competitors' Meta ads, and keep the results
   in the user's Adlicio history and brands.
3. Ask which product, competitor or market the user wants to understand. Then
   offer one first task that fits:
   - **A physical product:** the 1 to 3 star reviews on the product's or a
     competitor's Amazon listing, through `scrape_url`.
   - **An app or a game:** App Store, Google Play or Steam reviews, through
     `scrape_url`.
   - **Software or a service:** Trustpilot or G2 reviews through `scrape_url`,
     and Hacker News threads through `search_hackernews`.
   - **A problem or a niche:** `research_topic` for what people say on Reddit.
   - **Competitor ads:** `find_competitor_ads` for a brand or a niche.
   - **Work the user already did:** `list_history` and `search_history`, which
     cost 0 credits.

Each tool's description states its credit cost. Say the cost before any call
that costs more than 1 credit. Some tools need a higher plan. When a tool
returns `upgrade_required`, pass its message on to the user and do not retry.

Quote customers verbatim and keep each source link. Never invent a quote or a
link.
