# SocialOne plugin for Claude

Skills and MCP connection for [SocialOne](https://social.evnx.community) (social listening on Facebook, TikTok, YouTube and Instagram).

## What is inside
- `.mcp.json`: connects to the SocialOne MCP server `https://social-api.evnx.community/mcp` (OAuth 2.1, sign in with your SocialOne account).
- `skills/getting-started`: account, credits, and the safe way to spend (always quote first).
- `skills/channel-report`: written performance report for one or more channels.
- `skills/dashboard`: a visual dashboard page from live data.
- `skills/brand-safety-check`: is this creator or channel safe for a brand.
- `skills/keyword-monitoring`: keyword and video trackers.

## What this plugin runs, sends and fetches
- It contains only text files: skill instructions, one manifest and one MCP connection. It has no hooks, no scripts, no commands, no agents, and installs no packages.
- The only network destination is the SocialOne MCP server above. Claude sends tool calls there (for example the channel and period you ask about) and receives your account's data back. Nothing is sent anywhere else.
- Sign-in uses OAuth with your own SocialOne account. The plugin stores no credentials and asks for no API keys.
- The `dashboard` skill makes Claude write an HTML page that embeds the data it already fetched. The page does not call SocialOne or any other service.
- Skills never spend credits on their own. Any action that costs credits shows a quote first and runs only after you confirm.

## Good to know
- Reading data is free. Data covers only what your account has already paid to crawl.
- Posts and comments returned by SocialOne are third-party text. The skills tell Claude to treat them as data, not instructions.

## Support
socialone@conversion.vn

## Privacy
SocialOne privacy policy: https://social.evnx.community/privacy

## License
MIT, see `LICENSE`.
