---
name: brand-safety-check
description: Check whether a creator or channel looks safe for a brand, using SocialOne's brand-safety level, sentiment and the brand-safety result of each post. Use when the user asks if a creator is safe to work with, wants to screen a shortlist, or asks about risky content on their channels.
---

# Brand-safety check

SocialOne's AI scores each channel's recent posts (last 90 days) for brand-safety risks and exposes the result on every channel. (Content AI Guard, the older alert feed, was retired on 2026-11-27: its tools are gone.)

## Steps
1. Find the channel. For "the biggest channel" or "my top creators" use `get_portfolio_overview` (`platform`, `top`), which already shows each channel's brand-safety level. For a named creator ask for the link or id and use `get_channel`; scan `list_channels` (with `fields`) only as a last resort, because a large account has thousands of channels. Always pass `platform`. If the creator is not in the account, say so. Adding it costs credits, so follow the quote-first rule from `getting-started` and only do it if the user wants it.
2. Read `brand_safety` and `sentiment` from the channel's analytics:
   - The **level** is one of Safe, Stable, Acceptable, Risky or Unknown. Unknown usually means the channel has not been scanned enough yet (a new channel, or too few posts). Report that, and never treat Unknown as safe.
   - **Sentiment** shares are null when fewer than 10 posts were checked.
3. For a Facebook channel, see which posts were flagged and why: `list_post_safety` with `channel_id` (default medium and high; `min_level: low` for everything). Each row has the level, the flagged categories with a short reason (usually Vietnamese) and the post id; open the post with `get_post` when the user wants to see it. `flagged_only: false` also lists clean posts, which tells "checked and clean" apart from "never checked" (a post with no row was never checked).
4. Look at the content itself: `list_content_entities` (topics, brands, hashtag keywords) and the latest posts with `list_channel_posts` to spot sponsored content, competing brands or topics the brand avoids.
5. For several creators, build a table: creator, platform, followers, level, sentiment, number of high-risk posts, notes.

## Answer layout
- Verdict in one line (for example "Acceptable, no high-risk posts in 90 days"), then the evidence: level, sentiment, flagged posts with their reasons, example posts.
- Say how fresh and how complete the data is (window, posts checked, sync status).
- This is a screening aid, not a legal or contractual guarantee. Say so when the user is about to commit.
