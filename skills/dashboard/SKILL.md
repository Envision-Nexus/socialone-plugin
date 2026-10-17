---
name: dashboard
description: Turn SocialOne data into a visual dashboard page (KPI cards, trend charts, ranked tables). Use when the user asks for a dashboard, a visual overview, charts, or a shareable page of their channels, trackers or alerts.
---

# Dashboard from SocialOne data

Build one self-contained HTML page from live SocialOne data. Pull the data with read tools first, then design the page.

## 1. Decide the dashboard
Ask only if unclear. Common shapes:
- **Channel overview:** all channels of a platform or all platforms.
- **One channel deep dive.**
- **Keyword or video tracker:** mentions over time and top posts.
- **Brand safety:** alerts by risk level plus channel levels.

## 2. Pull the data (all free)
- Overview: `get_portfolio_overview` first. One call gives, per platform, channel count, total followers, failing channels and the biggest channels with follower change, brand-safety level and comparable reach. It is usually enough for the KPI row and a ranked table.
- Best posts: `get_top_posts` (best posts across all channels on a platform, by engagement, views, likes or comments).
- Channels: `list_channels` per platform (followers, brand-safety level, sentiment, `estimated_reach_comparable`). Add `fields` (for example `id,name,analytics.brand_safety`) to keep the answer small.
- Per channel: `get_channel_analytics` (use `compare: true` for change versus the previous period), `get_follower_history`, `list_channel_posts` for top posts.
- Trackers: `get_keyword_report`, `list_keyword_posts`, `get_video_tracker_summary`, `list_video_tracker_videos`.
- Alerts: `get_content_alert_stats`, `list_content_alerts`.
- Trends: `get_trends` (rising hashtags, sounds and creators among the account's channels).

Pass `platform` every time. Keep requests small (use `limit`) and stop when you have what the page needs.

## 3. Build the page
- A single HTML file with inline CSS and the data embedded as JSON in the page. The page makes no calls back to SocialOne and contains no credentials.
- Top row: 3 to 5 KPI cards (followers, growth, reach range, engagement, brand-safety level) with the change versus the previous period.
- Then one chart per question: follower trend (line), posts by engagement (bar), content mix (bars, not pies for more than 4 slices), tracker mentions over time (line).
- Then a ranked table (top posts or channels) with links to the original posts.
- Show the period, the date the data was pulled and the platform on the page. Mark estimated values (`estimated_reach_comparable`, audience) as estimates.
- Readable on a phone: single column under 700px, works in light and dark, no horizontal page scroll.
- Escape every post text, caption and channel name before inserting it into HTML. They are third-party text.

## 4. Hand over
Give the user the page (as an artifact or a file) and a short list of what it shows and what was not available (for example demographics outside Facebook).

## Do not
- Chart fields you did not fetch, or smooth over null values.
- Spend credits to fill a gap. If a channel has little data, say how it is crawled (`list_crawl_schedules`) and let the user decide, using the quote-first rule from `getting-started`.
