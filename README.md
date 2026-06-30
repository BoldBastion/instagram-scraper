[Instagram Scraper](https://apify.com/pear_fight/instagram-scraper?fpr=data)

# 📸 Instagram Profile & Post Scraper

Scrape Instagram profiles and posts at scale. Extract follower counts, bios, verification status, post captions, likes, comments, hashtags, and more.

## Features

- **Profile scraping** — username, full name, bio, followers, following, post count, verification badge, profile picture, external URL
- **Post scraping** — shortcode, caption, likes, comments, timestamp, image/video URLs, location, hashtags
- **Automatic post discovery** — optionally crawl posts directly from each profile's grid
- **Anti-detection** — residential proxy support + browser fingerprint injection
- **Full JS rendering** — Playwright-based, handles Instagram's dynamic SPA

## Input

| Field | Type | Default | Description |
| --- | --- | --- | --- |
| `profiles` | string[] | `[]` | Instagram usernames to scrape (without `@`) |
| `postUrls` | string[] | `[]` | Direct URLs to Instagram posts or reels |
| `maxPostsPerProfile` | integer | `12` | Max posts to scrape per profile (0–100) |
| `scrapePostsFromProfiles` | boolean | `true` | Also scrape posts from each profile's grid |
| `proxyConfig` | object | Residential | Apify proxy configuration |

### Example Input

```
{
  "profiles": ["instagram", "cristiano"],
  "postUrls": ["https://www.instagram.com/p/ABC123/"],
  "maxPostsPerProfile": 12,
  "scrapePostsFromProfiles": true,
  "proxyConfig": {
    "useApifyProxy": true,
    "apifyProxyGroups": ["RESIDENTIAL"]
  }
}
```

## Output

### Profile

```
{
  "type": "profile",
  "username": "cristiano",
  "fullName": "Cristiano Ronaldo",
  "bio": "Football player...",
  "followers": 620000000,
  "following": 583,
  "posts": 3600,
  "isVerified": true,
  "profilePicUrl": "https://...",
  "externalUrl": "https://...",
  "scrapedAt": "2026-02-21T12:00:00.000Z"
}
```

### Post

```
{
  "type": "post",
  "id": "ABC123",
  "shortcode": "ABC123",
  "caption": "Great day! #blessed",
  "likes": 5000000,
  "comments": 45000,
  "timestamp": "2026-02-20T15:30:00.000Z",
  "imageUrl": "https://...",
  "videoUrl": "",
  "isVideo": false,
  "location": "Madrid, Spain",
  "hashtags": ["blessed"],
  "postUrl": "https://www.instagram.com/p/ABC123/",
  "profileUsername": "cristiano",
  "scrapedAt": "2026-02-21T12:00:00.000Z"
}
```

## Tips

- **Use residential proxies** — Instagram aggressively blocks datacenter IPs. The default configuration uses Apify residential proxies.
- **Login walls** — Instagram may show login prompts for some content. The scraper extracts as much as possible from public meta tags and structured data.
- **Rate limiting** — Keep `maxPostsPerProfile` reasonable to avoid triggering blocks. Start with 12 and increase gradually.

## Cost Estimation

The actor uses Playwright with Chromium, so it consumes more compute than simple HTTP scrapers. Rough estimate: ~$0.25–0.50 per 100 results depending on proxy usage.

## License

Apache-2.0