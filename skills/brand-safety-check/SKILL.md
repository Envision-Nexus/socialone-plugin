---
name: brand-safety-check
description: Check whether a creator or channel looks safe for a brand, using SocialOne's brand-safety level, sentiment and Content AI Guard alerts. Use when the user asks if a creator is safe to work with, wants to screen a shortlist, or asks about risky content on their channels.
---

# Brand-safety check

SocialOne scores each channel's recent posts (last 90 days) and exposes the result on every channel.

## Steps
1. Find the channel with `list_channels` (or `get_channel` if the id is known). Always pass `platform`. If the creator is not in the account, say so. Adding it costs credits, so follow the quote-first rule from `getting-started` and only do it if the user wants it.
2. Read `brand_safety` and `sentiment` from the channel's analytics:
   - The **level** is one of Safe, Stable, Acceptable, Risky or Unknown. Unknown usually means the channel has not been scanned enough yet (a new channel, or too few posts). Report that, and never treat Unknown as safe.
   - **Sentiment** shares are null when fewer than 10 posts were checked.
3. For Facebook channels guarded by Content AI Guard: `list_content_alerts` with `channel_id` and `risk_level`, and `get_content_alert_stats` for counts. Open `get_content_alert` for any high-risk alert to see the flagged post.
4. Look at the content itself: `list_content_entities` (topics, brands, hashtag keywords) and the latest posts with `list_channel_posts` to spot sponsored content, competing brands or topics the brand avoids.
5. For several creators, build a table: creator, platform, followers, level, sentiment, number of high-risk alerts, notes.

## Answer layout
- Verdict in one line (for example "Acceptable, no high-risk alerts in 90 days"), then the evidence: level, sentiment, alert counts, example posts.
- Say how fresh and how complete the data is (window, posts checked, sync status).
- This is a screening aid, not a legal or contractual guarantee. Say so when the user is about to commit.

## Managing alerts
Only when asked: `set_alert_ignored` dismisses or restores one alert, and `set_guard_channel` turns scanning on or off for a Facebook channel. These change the account, so confirm first.
