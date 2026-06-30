[Instagram Scraper](https://apify.com/thirdwatch/instagram-scraper?fpr=data)

# Instagram Scraper

> Scrape Instagram posts and profiles without a login — captions, like and comment counts, media URLs, follower counts, and recent post history.

## What you get

Structured data for any public Instagram account or post. Pass usernames, post URLs, or hashtag-prefixed search terms and get back engagement metrics, media links, and profile metadata. When scraping profiles you also get the most recent N posts per profile for content and engagement analytics.

## Output fields (posts)

| Field | Description |
| --- | --- |
| `shortcode` | Post shortcode (used in the URL) |
| `url` | Full post URL |
| `type` | `image`, `video`, `carousel`, or `reel` |
| `caption` | Post caption text |
| `likeCount` | Number of likes |
| `commentCount` | Number of comments |
| `viewCount` | View count (video/reel) |
| `authorUsername` | Author handle |
| `timestamp` | ISO 8601 post timestamp |
| `location` | Tagged location (if any) |
| `imageUrl` | Full-resolution image URL |
| `videoUrl` | Video URL (if video/reel) |
| `hashtags` | Hashtags extracted from the caption |

## Output fields (profiles)

| Field | Description |
| --- | --- |
| `username` | Instagram username |
| `fullName` | Display name |
| `biography` | Profile bio |
| `followerCount` | Number of followers |
| `followingCount` | Number of accounts followed |
| `postCount` | Total posts |
| `isVerified` | Verified badge flag |
| `isPrivate` | Private-account flag |
| `profilePicUrl` | Profile picture URL |
| `externalUrl` | Link in bio |
| `recentPosts` | Array of recent posts (up to `maxPostsPerProfile`) |

## Example output

```
{
    "shortcode": "C7xYz12ABcd",
    "url": "https://www.instagram.com/p/C7xYz12ABcd/",
    "type": "image",
    "caption": "Sunrise at the South Rim. #nature #photography",
    "likeCount": 245000,
    "commentCount": 1200,
    "authorUsername": "natgeo",
    "timestamp": "2026-04-08T18:30:00+00:00",
    "location": "Grand Canyon National Park",
    "imageUrl": "https://scontent.cdninstagram.com/...",
    "hashtags": ["nature", "photography"]
}
```

## Input parameters

| Parameter | Required | Description |
| --- | --- | --- |
| `queries` | Yes | List of `@username`, `#hashtag`, post URLs, or profile URLs. Examples: `["@natgeo", "#photography", "https://www.instagram.com/p/ABC123/"]`. |
| `searchType` | No | `posts` returns individual posts/media, `profiles` returns profile info with recent posts. Default `posts`. |
| `maxResults` | No | Max total results across all queries. Default `8`. |
| `maxResultsPerQuery` | No | Max results per individual query. `0` = no per-query limit. Default `0`. |
| `maxPostsPerProfile` | No | When `searchType=profiles`, recent posts returned per profile. Default `12`, max `60`. |

## Use cases

- **Social media marketers**: Benchmark competitor content, post cadence, and engagement.
- **Influencer analysts**: Pull follower counts and recent-post engagement for creator shortlists.
- **Brand monitoring**: Watch hashtag feeds and profile activity for mentions.
- **Trend researchers**: Collect caption and hashtag corpora for NLP and topic modeling.
- **CRM enrichment**: Attach Instagram metrics to creator and influencer records.

 

## Use cases & recipes

Step-by-step guides on [thirdwatch.dev/blog](https://thirdwatch.dev/blog):

- [Monitor Brand Instagram Engagement (2026 Guide)](https://thirdwatch.dev/blog/monitor-brand-instagram-engagement)
- [Research Instagram Hashtag Performance (2026 Guide)](https://thirdwatch.dev/blog/research-instagram-hashtag-performance)
- [Scrape Instagram Profiles and Posts at Scale (2026)](https://thirdwatch.dev/blog/scrape-instagram-profiles-and-posts)
- [Track Influencer Follower Growth on Instagram (2026)](https://thirdwatch.dev/blog/track-influencer-follower-growth-on-instagram)

 -end

## Pricing

Pay-per-result pricing. Tiered discounts apply automatically based on usage volume.

| Tier | Price per result |
| --- | --- |
| FREE | $0.006 |
| BRONZE | $0.005 |
| SILVER | $0.004 |
| GOLD | $0.003 |

## Limitations

- Private profiles cannot be scraped.
- Stories and the Reels "For You" feed require authentication and are not supported.
- Hashtag and location search are rate-limited in 2026 and may return partial results.
- `viewCount` is only populated for video and reel posts.

## Compared to alternatives

- **vs. apify/instagram-scraper** ($0.0027/result, 224K users): That actor is cheaper per result. This one is priced higher but ships a single consolidated schema across posts and profiles, includes `maxPostsPerProfile` for recent-post enrichment, and is maintained on a predictable release cadence.

Pairs well with [TikTok Scraper](https://apify.com/thirdwatch/tiktok-scraper) and [YouTube Scraper](https://apify.com/thirdwatch/youtube-scraper) for cross-platform creator research.

## FAQ

**Can I scrape a single post by URL?**
Yes. Pass the `https://www.instagram.com/p/...` URL directly in `queries`.

**Can I get recent posts from a profile?**
Yes. Set `searchType: "profiles"` and use `maxPostsPerProfile` to control how many recent posts come back per profile.

**Do I need an Instagram account or API key?**
No. The actor works against publicly accessible endpoints.

**Will it scrape Stories or Reels tab?**
No. Stories require login. Individual reels that appear in a profile's grid are returned as posts with `type: "reel"`.

Last verified: 2026-04

More scrapers at [thirdwatch.dev](https://thirdwatch.dev).