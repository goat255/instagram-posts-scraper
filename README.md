# Instagram Posts Scraper

Find out which posts actually work. Pull every post from any list of Instagram accounts with full captions, likes, comments, video views, media URLs, tagged users, collaborators and paid-partnership flags. No Instagram login, no cookies, no API key.

[![Watch the demo on YouTube](https://img.youtube.com/vi/hPGnOaRcqIA/maxresdefault.jpg)](https://www.youtube.com/watch?v=hPGnOaRcqIA)

**[Run it on Apify →](https://apify.com/goat255/instagram-posts-scraper)**

## What you get

For each post:

- **Engagement**: `likeCount`, `commentCount` and `videoViewCount`, so you can rank posts by what people responded to.
- **Content**: the full `caption` with hashtags and mentions, `mediaType` (`image`, `video` or `carousel`), `timestamp` and `location`.
- **Media**: `displayUrl`, `thumbnailUrl`, `videoUrl`, and every carousel slide in `children`.
- **People**: `taggedUsers`, `coauthors` and the `isPaidPartnership` flag for sponsored content.
- **Every row carries its `username`**, so multi-account runs group and filter cleanly.

```json
{
  "username": "example_user",
  "shortcode": "ABC123xyz",
  "url": "https://www.instagram.com/p/ABC123xyz/",
  "mediaType": "video",
  "timestamp": 1767225600,
  "caption": "Behind the scenes of our spring launch #acme",
  "likeCount": 18420,
  "commentCount": 312,
  "videoViewCount": 245000,
  "isReel": true,
  "taggedUsers": ["another_example"],
  "coauthors": [],
  "isPaidPartnership": false,
  "displayUrl": "https://example.com/post.jpg"
}
```

## What people use it for

- Content strategy: find the best posts in your niche and see what they have in common.
- Brand monitoring: track every post an account publishes and how it performs.
- Influencer vetting: measure real engagement across an account's recent posts.
- Sponsored content audits: spot paid partnerships with `isPaidPartnership`.

## Run it

From the Apify Console, add one or more usernames, set how many posts you want per account and press Start. Use `onlyPostsNewerThan` to keep only recent posts; it filters by each post's real date, so old pinned posts stay out. Or call it from code:

```bash
curl -X POST "https://api.apify.com/v2/acts/goat255~instagram-posts-scraper/run-sync-get-dataset-items?token=YOUR_APIFY_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"usernames": ["example_user"], "maxPostsPerUser": 50, "onlyPostsNewerThan": "2026-01-01"}'
```

## Use it from an AI agent

Works with Claude, Codex and any agent that speaks MCP or HTTP. See [AGENTS.md](AGENTS.md) for the input, output and a ready-made MCP setup.

## Pricing

Pay per post returned. Current prices are on the [Apify Store page](https://apify.com/goat255/instagram-posts-scraper).

## More actors

This page is a showcase; the actor itself runs on Apify. **[Check our profile for more such actors →](https://apify.com/goat255)**
