---
name: adlicio-forum-answers
description: >-
  Find the forum threads people land on from Google for the questions a product
  answers (Reddit, Quora, Facebook groups, LinkedIn, Stack Exchange and
  community forums), check which still take replies, and draft honest answers
  that disclose the product. Use when the user wants to answer questions on
  forums, Quora or Reddit about their topic, find old threads that still rank
  on Google or get cited in AI answers, or get traffic from forum replies.
---

# Forum answers

Goal: a short, ranked list of open threads that rank on Google for the user's questions, each with a draft answer the user posts under their own name.

1. Product. Ask what they sell, who buys it, and the pages an answer can link to (free tools, guides, pricing). If they have Search Console queries, ask for the top 10 to 20.
2. Queries. Write 10 to 20 Google searches in three groups, phrased the way people search and without the user's brand name:
   - Buyer questions: the problem a paying customer has ("how to find customer pain points for ad copy", "best <category> tool", "<competitor> alternative").
   - How-to questions: tasks the product does ("how to export instagram comments", "how to add mcp to chatgpt").
   - Tool searches: what people type to find a tool like it ("instagram comment viewer").
3. Search. Call `find_forum_threads` with up to 10 queries per call (1 credit per call). Run a second call for the rest.
4. Pick. Keep threads with status open or likely_open whose question the product truly answers. Drop closed and likely_archived threads, posts that promote another tool, threads on unrelated forums, and Stack Overflow or Apple Community (they remove tool recommendations). Rank buyer threads first, then how-to, then tool threads; within each group, threads that the AI Overview cites or that rank for several queries come first.
5. Read. Call `scrape_url` on the top threads to read the question and the replies already there. Add what the existing replies miss; do not repeat them.
6. Draft one answer per thread, in the user's voice:
   - Answer the question fully first, with steps that work without the product.
   - Then one line that names the product, says plainly that the user built it, and links the one page that fits the question.
   - Fit the site: Quora 100 to 200 words; Reddit shorter and casual, with no link where the subreddit rules forbid links; LinkedIn comments 2 to 4 sentences without a link; Facebook groups short.
   - Never reuse the same text for two threads. Do not invent numbers, results or personal stories; state only what the product page says.
7. Output. A table (priority, thread, platform, best Google position, status), then the drafts, each under its thread link. Remind the user to post from one real account, at most 3 answers a day per site, and to check that a thread still takes replies before posting.

Never post for the user, never write from several accounts, and never write an answer that hides the user's connection to the product.
