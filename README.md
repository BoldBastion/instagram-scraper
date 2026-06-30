[Instagram Scraper](https://apify.com/aimscrape/instagram-scraper?fpr=data)

# Instagram Scraper: Profiles, Reels, Tagged, Audio, Locations, Hashtags

This Actor collects **public Instagram posts and reels** from multiple discovery surfaces, including profiles, reels tabs, tagged tabs, audio/music pages, locations, hashtags, and direct post/reel URLs. No login is required.

It is optimized for fast, post-level output: list pages are used to discover shortcodes, then each discovered item is normalized into one dataset record.

## What you get

Each dataset item is one Instagram post/reel record with `url` and related metadata.

Supported discovery inputs:

- Profiles: `username` or `https://www.instagram.com/{username}/`
- Reels tab: `https://www.instagram.com/{username}/reels/`
- Tagged tab: `https://www.instagram.com/{username}/tagged/`
- Audio/Music: `https://www.instagram.com/reels/audio/{audio_id}/`
- Locations: `https://www.instagram.com/explore/locations/{location_id}/...`
- Hashtags: `https://www.instagram.com/popular/{hashtag}/`
- Direct links: `https://www.instagram.com/p/{shortcode}/` or `https://www.instagram.com/reel/{shortcode}/`

Common output fields:

- `id`, `pk`, `shortcode`, `url`, `from_url`: identifiers and source context
- `is_video`, `image`, `video_url`, `has_audio`, `video_duration`: media type and media URLs
- `caption`, `accessibility_caption`, `hashtags`, `mentions`, `tagged_user`: text and entity extraction
- `comment_count`, `like_count`, `play_count`, `view_count`: engagement metrics (nullable)
- `comments`: optional top-level comment previews (only when included in post detail responses)
- `owner`, `coauthor_producers`: author/co-author objects (when available)
- `location`, `product_type`, `clips_music_attribution_info`: post metadata
- `taken_at`, `crawled_at`: content timestamp (UTC ISO) and scrape timestamp (ISO)

Notes about `comments`:

- `comments` is a **preview list**, not a full comments scraper (no pagination).
- Only **top-level** comments are included (replies are not included).
- The field may be **omitted** on some items; restricted/fallback items may include `comments: null`.

Notes about `url`:

- `url` is the preferred canonical post link.

## Other Scrapers

If you also collect YouTube data, these Actors are a good match:

| Scraper | Best for | Output highlights |
| --- | --- | --- |
| [Fast YouTube Channel Video Scraper](https://apify.com/aimscrape/youtube-channel-video-scraper) | Collecting videos from a specific channel's `/videos` page | Video URL/ID, title, thumbnail, views text, publish date |
| [YouTube Advanced Search Scraper](https://apify.com/aimscrape/youtube-search-video-scraper) | Collecting videos from keyword-based YouTube search results | Normalized video list with duration and channel metadata |

## How to run it in the Apify Console

1. Open the Actor page and click **Try for free / Run**.
2. In **Input**, paste one or more Instagram queries (username/profile/reels/tagged/post/reel/audio URLs).
3. Optionally set the maximum number of posts to collect per query in **Input** (see schema).
A query is one input line, such as a username, profile tab URL (reels/tagged), audio URL, hashtag URL, location URL, or a direct post/reel URL.
4. After the run finishes, open the **Dataset** to view results and export to JSON / CSV / Excel.

## Input

### `queries` (required)

Example:

```
username
https://www.instagram.com/p/{shortcode}/
https://www.instagram.com/reel/{shortcode}/
https://www.instagram.com/google
https://www.instagram.com/google/reels/
https://www.instagram.com/google/tagged/
https://www.instagram.com/reels/audio/502550169096496/
https://www.instagram.com/explore/locations/215631076/williamsburg/
https://www.instagram.com/explore/locations/215631076/williamsburg/recent/
https://www.instagram.com/popular/furniture/
```

Notes:

- Empty/blank entries are ignored and inputs are de‑duplicated
- Unsupported/invalid usernames or URLs are skipped and reported in logs (no charge; they do not automatically fail the whole run)
- `location` only support top and recent（recent max results 18; top varies by location/time and IG behavior）

### Example input

```
{
  "queries": ["youtube", "https://www.instagram.com/google"]
}
```

Example output (truncated):

```
{
  "id": "3849765618028134045",
  "pk": "3849765618028134045",
  "is_video": true,
  "video_url": "https://instagram.fhkg4-2.fna.fbcdn...=69B586DC",
  "has_audio": true,
  "video_duration": 93.013,
  "accessibility_caption": null,
  "hashtags": [],
  "mentions": [],
  "tagged_user": [
    {
      "full_name": "Google",
      "followed_by_viewer": false,
      "id": "1067259270",
      "is_verified": true,
      "profile_pic_url": "https://instagram.fhkg4-2.fna...=d885a2",
      "username": "google"
    }
  ],
  "caption": "Want to know how the pros use AI? 💡 Google Docs Product Manager Frank Tisellano takes us through the new Gemini features launching today that help you draft, polish, and align your writing effortlessly. ✍️✨",
  "comment_count": 46,
  "comments": [
    {
      "id": "17982927302966768",
      "text": "Nice post!",
      "created_at": 1772855351,
      "did_report_as_spam": false,
      "owner": {
        "id": "66485496816",
        "is_verified": false,
        "profile_pic_url": "https://example.com/profile.jpg",
        "username": "some_user"
      },
      "viewer_has_liked": false,
      "like_count": 0,
      "is_restricted_pending": false
    }
  ],
  "like_count": 943,
  "play_count": 892753,
  "view_count": 27179,
  "taken_at": "2026-03-10T13:10:16Z",
  "is_ad": false,
  "is_affiliate": false,
  "is_paid_partnership": false,
  "is_published": true,
  "location": null,
  "from_url": "https://www.instagram.com/google/",
  "url": "https://www.instagram.com/reel/DVtHW7DFD6d/",
  "crawled_at": "2026-03-13T05:50:18.141550Z",
  "image": "https://instagram.fhkg..._nc_sid=d885a2",
  "shortcode": "DVtHW7DFD6d",
  "product_type": "clips",
  "clips_music_attribution_info": {
    "artist_name": "googleworkspace",
    "song_name": "Original audio",
    "uses_original_audio": true,
    "should_mute_audio": false,
    "should_mute_audio_reason": "",
    "audio_id": "26560146256910882"
  },
  "owner": {
    "id": "46028029670",
    "username": "googleworkspace",
    "is_verified": true,
    "profile_pic_url": "https://instagram.fhk...id=d885a2",
    "blocked_by_viewer": false,
    "restricted_by_viewer": null,
    "followed_by_viewer": false,
    "full_name": "Google Workspace",
    "has_blocked_viewer": false,
    "is_embeds_disabled": false,
    "is_private": false,
    "is_unpublished": false,
    "requested_by_viewer": false,
    "pass_tiering_recommendation": true,
    "post_count": 1554,
    "followers": 586669
  },
  "coauthor_producers": [
    {
      "id": "1067259270",
      "is_verified": true,
      "profile_pic_url": "https://instagra...c_sid=d885a2",
      "username": "google"
    }
  ]
}
```

## FAQ

### 1) Why is the Dataset empty / much smaller than expected?

Common reasons:

- The query is invalid/unsupported and was skipped (check run logs)
- The source has fewer public posts/reels than requested
- The profile is private or restricted for anonymous (no-login) access
- Instagram is temporarily limiting anonymous requests on that source

### 2) What does `Restricted profile` mean?

A profile can be public but still limit anonymous access.
Instagram may gate some endpoints unless a logged-in session is used.
When this happens, the Actor logs the restriction and skips or stops that profile source.

### 3) Why are some fields `null`?

Some values are not consistently exposed by Instagram for every post or source.
Fields such as `video_duration`, `play_count`, `view_count`, `location`, or music metadata may be `null`.
This is expected behavior for public, no-login scraping.

## Limitations & recommendations

- **Data scope**: this Actor returns post/reel items (not full profile documents).
- **Access limits**: some sources and fields are unavailable or unstable for anonymous (no-login) access, even on public accounts/pages.
- **Dynamic surfaces**: location/hashtag/reels/tagged pages are dynamic, so results can vary over time for the same query.
- **Compliance**: make sure your usage complies with Instagram's terms and local laws, and only collect data you have the right to use.