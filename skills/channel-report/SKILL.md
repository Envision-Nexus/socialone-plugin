---
name: channel-report
description: Build a written performance report for one or several SocialOne channels (followers, growth, reach, engagement, top posts, brand safety). Use when the user asks how a channel or creator is doing, wants a weekly or monthly report, or wants to compare channels.
---

# Channel report

Produce a short report the user can read in a minute. Reading is free, so gather what you need.

## Steps
1. **Pick the channels.** If the user named them, find them with `list_channels` (per platform). If not, list the channels and ask which ones, or report on the top few by followers.
2. **Pick the period.** Default to the last 30 days. Use `YYYY-MM-DD` dates.
3. **Per channel, collect:**
   - `get_channel`: profile, followers, category, sync status, and headline analytics (brand-safety level and sentiment, `estimated_reach_comparable`).
   - `get_channel_analytics` with `start_date`, `end_date` and `compare: true`: KPIs with change versus the previous period, reach, best posting times, content breakdown.
   - `get_follower_history` for the follower curve.
   - `list_channel_posts` with `since`/`until` for the period. It lists oldest first, so page with `after` until the window is covered. Pick the top posts by engagement yourself.
4. **Compare channels.** `compare_channels` takes 2 to 4 channels but only works for Facebook. For other platforms, line the numbers up yourself using `estimated_reach_comparable` (one views-based scale across platforms).
5. **Facebook extras.** `get_audience_demographics` (gender, age, location, estimated). Other platforms have no demographics yet.

## Report layout
- One-line headline per channel: followers, change, standout.
- A small table across channels: followers, growth, average engagement, reach range, brand-safety level.
- Top 3 posts with a one-line reason each, and anything that dropped.
- Caveats: data window, `sync_status` problems, brand safety shown as unknown for channels not scanned yet, estimated numbers marked as estimates.

## Do not
- Invent numbers or fill gaps. If a field is null, say it is not available.
- Spend credits. This skill only reads. Suggest `onboard_channel` or a crawl tier only if the user asks how to get more data, and follow the quote-first rule from `getting-started`.
