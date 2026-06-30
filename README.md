[Instagram Scraper](https://apify.com/sovereigntaylor/instagram-scraper?fpr=data)

Extract data from public Instagram profiles, posts, and hashtags at scale. Scrape follower counts, bios, engagement metrics, captions, likes, comments, media URLs, and more. Built for influencer marketing, brand monitoring, competitor analysis, and social listening.

## What It Does

- **Profile scraping** — Enter usernames and get full profile data including follower counts, bio, post count, verified status, and profile picture
- **Post extraction** — Scrape recent posts with captions, like counts, comment counts, media URLs, timestamps, and video view counts
- **Hashtag exploration** — Discover trending posts under any hashtag for social listening and trend tracking
- **Comment collection** — Optionally scrape comments on posts for sentiment analysis and engagement research
- **Session cookie support** — Provide your Instagram session cookie for higher rate limits and access to more data

## Input Parameters

| Parameter | Type | Default | Description |
| --- | --- | --- | --- |
| `usernames` | array | `["natgeo"]` | Instagram usernames to scrape (without the @ symbol) |
| `hashtags` | array | `["technology"]` | Hashtags to explore (without the # symbol) |
| `maxPosts` | integer | `10` | Maximum number of posts to extract per profile or hashtag (max 1,000) |
| `includeComments` | boolean | `false` | Also scrape comments on each post |
| `sessionCookie` | string | — | Your Instagram `sessionid` cookie for authenticated access (optional but recommended) |
| `maxConcurrency` | integer | `1` | Number of parallel requests (keep at 1 for Instagram) |
| `proxyConfiguration` | object | `{"useApifyProxy": true}` | Proxy settings — **residential proxies strongly recommended** |

## Output Example

Profile data:

```
{
  "type": "profile",
  "username": "natgeo",
  "fullName": "National Geographic",
  "bio": "Experience the world through the eyes of National Geographic photographers.",
  "followerCount": 284000000,
  "followingCount": 156,
  "postCount": 32847,
  "isVerified": true,
  "isPrivate": false,
  "profilePicUrl": "https://scontent-iad3-1.cdninstagram.com/v/t51.2885-19/abc123_150x150.jpg",
  "externalUrl": "https://www.nationalgeographic.com",
  "dataSource": "json_ld",
  "scrapedAt": "2026-03-03T10:12:05.789Z",
  "url": "https://www.instagram.com/natgeo/"
}
```

Post data:

```
{
  "type": "post",
  "ownerUsername": "natgeo",
  "shortcode": "C4xR2bNJqMk",
  "caption": "Photo by @paulnicklen | A curious emperor penguin chick approaches the camera on the sea ice of Antarctica. These remarkable birds endure the harshest conditions on Earth.",
  "likesCount": 1245000,
  "commentsCount": 4832,
  "timestamp": "2026-02-28T15:30:00.000Z",
  "imageUrl": "https://scontent-iad3-1.cdninstagram.com/v/t51.2885-15/abc123_1080x1080.jpg",
  "videoUrl": null,
  "isVideo": false,
  "videoViewCount": null,
  "location": "Antarctica",
  "postUrl": "https://www.instagram.com/p/C4xR2bNJqMk/"
}
```

## Use Cases

- **Influencer marketing** — Analyze creator profiles, follower counts, and engagement rates before sponsorship deals
- **Brand monitoring** — Track mentions of your brand across hashtags and competitor accounts
- **Competitor analysis** — Compare posting frequency, engagement metrics, and content strategy across competitor profiles
- **Social listening** — Monitor hashtag trends and post volume for market sentiment and trending topics
- **Content research** — Discover top-performing posts in any niche for inspiration and content planning
- **Lead generation** — Find potential brand ambassadors by scraping profiles in your industry vertical

## API Usage

### JavaScript

```
import { ApifyClient } from 'apify-client';

const client = new ApifyClient({ token: 'YOUR_API_TOKEN' });
const run = await client.actor('sovereigntaylor/instagram-scraper').call({
    usernames: ['natgeo', 'nasa'],
    maxPosts: 50,
    includeComments: false,
});
const { items } = await client.dataset(run.defaultDatasetId).listItems();
console.log(items);
```

### Python

```
from apify_client import ApifyClient

client = ApifyClient('YOUR_API_TOKEN')
run = client.actor('sovereigntaylor/instagram-scraper').call(run_input={
    'usernames': ['natgeo', 'nasa'],
    'maxPosts': 50,
    'includeComments': False,
})
items = client.dataset(run['defaultDatasetId']).list_items().items
print(items)
```

### cURL

```
curl "https://api.apify.com/v2/acts/sovereigntaylor~instagram-scraper/runs" \
  -X POST \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer YOUR_API_TOKEN" \
  -d '{
    "usernames": ["natgeo", "nasa"],
    "maxPosts": 50,
    "includeComments": false
  }'
```

## Pricing

This actor uses pay-per-event pricing — you only pay for data successfully scraped.

| Event | Price |
| --- | --- |
| Profile scraped | $0.005 |
| Post scraped | $0.002 |
| Hashtag page scraped | $0.003 |

**Example:** Scraping 5 profiles + 250 posts = (5 x $0.005) + (250 x $0.002) = **$0.525**

## Limitations

- **Instagram is one of the hardest platforms to scrape** — residential proxies are essential for reliable results
- Private accounts cannot be scraped
- Without a session cookie, data is limited to what Instagram shows to logged-out visitors (profile info + recent posts only)
- Instagram rate-limits aggressively — keep `maxConcurrency` at 1 and expect slower scraping compared to other platforms
- Like and comment counts on very popular posts may be approximate (Instagram rounds large numbers)
- Stories, Reels metadata, and DM data cannot be scraped
- Hashtag scraping returns the "top posts" selection, not a complete chronological feed
- Maximum 1,000 posts per profile or hashtag per run

## Related Actors

- [Twitter/X Followers Scraper](https://apify.com/sovereigntaylor/twitter-followers-scraper) — Scrape follower lists and profile data from X/Twitter
- [YouTube Scraper](https://apify.com/sovereigntaylor/youtube-scraper) — Extract YouTube videos and channel metadata
- [Reddit Scraper](https://apify.com/sovereigntaylor/reddit-scraper) — Scrape Reddit posts and comments from any subreddit
- [TripAdvisor Scraper](https://apify.com/sovereigntaylor/tripadvisor-scraper) — Extract reviews and ratings from TripAdvisor