# AGENTS.md: Instagram Posts Scraper

Guide for AI agents (Claude, Codex, any MCP or HTTP client) that need Instagram posts.

## When to use it

Use this actor when a task needs the posts of one or more Instagram accounts with their engagement: content research, finding top-performing posts, brand monitoring, influencer vetting or sponsored-content audits. It does not post, follow or log in.

## Call it

**MCP (recommended):** add the Apify MCP server with this actor enabled:

```json
{
  "mcpServers": {
    "apify": {
      "url": "https://mcp.apify.com/?actors=goat255/instagram-posts-scraper",
      "headers": { "Authorization": "Bearer YOUR_APIFY_TOKEN" }
    }
  }
}
```

**HTTP:** one synchronous call returns the rows:

```
POST https://api.apify.com/v2/acts/goat255~instagram-posts-scraper/run-sync-get-dataset-items?token=YOUR_APIFY_TOKEN
Content-Type: application/json

{"usernames": ["example_user"], "maxPostsPerUser": 24}
```

## Input

| Field | Type | Default | Meaning |
|---|---|---|---|
| `usernames` | array of strings | required | Usernames, @handles or profile URLs, mixed freely |
| `maxPostsPerUser` | integer | `12` | Posts per account; `0` returns all available posts |
| `onlyPostsNewerThan` | string (YYYY-MM-DD) | none | Keep only posts on or after this date, by each post's real date |
| `concurrency` | integer | `5` | Accounts fetched in parallel (1 to 20) |
| `delayBetweenRequests` | number | `1.0` | Seconds to wait between requests |
| `proxyConfiguration` | object | residential | Leave the default on |

## Output: one row per post

| Field | Meaning |
|---|---|
| `username` | The account the post belongs to |
| `id`, `shortcode`, `url` | Post id, URL slug and link |
| `mediaType`, `isReel` | `image`, `video` or `carousel`; reel flag |
| `timestamp` | When it was posted (Unix seconds) |
| `caption`, `accessibilityCaption` | Full caption; alt text |
| `likeCount`, `commentCount`, `videoViewCount` | Engagement |
| `displayUrl`, `thumbnailUrl`, `videoUrl`, `dimensions` | Media |
| `children` | Carousel slides with their own media URLs |
| `location`, `taggedUsers`, `coauthors` | Place and people |
| `isPaidPartnership`, `commentsDisabled` | Sponsored flag; comments switched off |

## Tips for agents

- Batch many usernames into one run and group the rows by `username`.
- Pagination is automatic; ask for the number of posts you need with `maxPostsPerUser`.
- To find the best post, sort by `likeCount + commentCount`, or by `videoViewCount` for reels.
- Media URLs expire. Download the media soon after the run if you need to keep it.

Store page: https://apify.com/goat255/instagram-posts-scraper
