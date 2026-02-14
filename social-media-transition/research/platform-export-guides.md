# Platform Data Export Guide

**Status:** Research Phase
**Goal:** Document data export capabilities for all major social platforms

---

## Meta (Facebook, Instagram, WhatsApp)

### Facebook
**Tool:** Download Your Information (DYI)
- **URL:** https://www.facebook.com/dyi
- **Data Available:** Posts, photos, videos, messages, ads, profile info, friends list
- **Format:** HTML, JSON
- **Time:** Minutes to days (depending on data volume)
- **Physical Media:** ~~CD/DVD service discontinued~~ (2012-2018 available, now digital-only)
- **Limitations:** Does NOT include:
  - Comments on others' posts
  - Shared posts metadata
  - Real-time location history
  - Note: Large archives (>5GB) split into multiple ZIP files - user must burn to CD/DVD themselves

### Instagram
**Tool:** Data Download
- **Path:** Settings → Security → Download Data
- **Data Available:** Photos, videos, Stories, messages, profile info, comments
- **Format:** JSON
- **Physical Media:** Never offered - digital-only since launch
- **Limitations:**
  - Stories only available if archived
  - Direct messages: text only, no media
  - No bulk export of saved posts/collections
  - Videos in reduced quality

### WhatsApp
**Tool:** Chat Export
- **Path:** Individual chat → Export Chat
- **Format:** .txt (with media as separate files)
- **Limitations:**
  - NO full account export
  - Must export chats individually
  - Media not included in default export
  - Encrypted backups not exportable as readable format

---

## X (Twitter)

### Official Archive (Recommended for Complete Export)
**Tool:** Download Archive
- **Path:** Settings → Your Account → Download an archive
- **URL:** https://x.com/settings/download_your_data
- **Data Available:** ALL tweets since account creation, DMs, likes, lists, moments
- **Format:** JSON, HTML interface
- **Time:** 24 hours to several days
- **Cost:** FREE
- **Limitations:**
  - No export of deleted tweets
  - Archived tweets need desktop app to view properly
  - Processing time varies by account size

### API v1.1 (Legacy)
**Endpoint:** `GET statuses/user_timeline`
- **URL:** https://developer.twitter.com/en/docs/twitter-api/v1/tweets/timelines/api-reference/get-statuses-user_timeline
- **Hard Limit:** 3,200 most recent tweets per user (maximum)
- **Rate Limit:** 1,500 requests / 15 minutes (app auth)
- **Pagination:** 200 tweets per request (max)
- **Key Point:** Limit is **per account**, not per session or API key

### API v2 (Premium)
- **URL:** https://developer.x.com/en/products/x-api
- **Pricing:** Pay-per-usage (no monthly subscriptions)
- **Basic Tier ($100/month):** 10,000 tweets/month read limit
- **Pro Tier ($5,000/month):** 1,000,000 tweets/month read limit
- **Advantage:** Can access historical tweets beyond 3,200 limit

### Workarounds for 3,200 Tweet Limit

#### 1. Multiple API Keys (Limited Effectiveness)
- Creating multiple apps/keys does **NOT** bypass the 3,200 limit
- The limit is tied to the **user account**, not the API key
- Multiple keys only help with rate limiting (requests per 15 min)

#### 2. Official Archive Download (Best Option)
- Only way to get ALL tweets (not just recent 3,200)
- Free, but takes days to process
- JSON format requires parsing for analysis

#### 3. Third-Party Services
| Service | Cost | Features | URL |
|---------|------|----------|-----|
| **ExportData.io** | ~$20 | Complete export, various formats | https://www.exportdata.io |
| **TweetDownload.net** | Free/Paid | PDF, CSV, Excel exports | https://www.tweetdownload.net |
| **AllMyTweets.net** | Free | View all tweets (not download) | https://www.allmytweets.net |

#### 4. Wayback Machine
- **URL:** https://web.archive.org
- Only captures public tweets that were archived
- Spotty coverage, not comprehensive

### Practical IT Consulting Workflow

```
For complete X export:
1. Request native archive (FREE, 1-7 days wait)
   → Contains all tweets, DMs, media since account creation
   
2. For current/active data (last 3,200 tweets)
   → Use API v1.1 or v2 for real-time tools
   
3. For historical gaps (if archive incomplete)
   → Use third-party services like ExportData.io
```

### Rate Limit Reference
| Endpoint | Limit | Window |
|----------|-------|--------|
| user_timeline | 1,500 requests | 15 minutes |
| user_timeline | 3,200 tweets max | Account lifetime (hard limit) |
| home_timeline | 15 requests | 15 minutes |
| mentions_timeline | 75 requests | 15 minutes |

---

## LinkedIn

### Data Export
**Tool:** Download your data
- **Path:** Settings → Data privacy → Get a copy
- **Data Available:** Profile, connections, messages, recommendations
- **Format:** CSV (connections), HTML (profile)
- **Limitations:**
  - Messages: text only
  - No bulk export of saved articles
  - Network insights not exportable

---

## TikTok

### Data Request
**Tool:** Download your data
- **Path:** Settings → Privacy → Download your data
- **Data Available:** Videos, comments, profile, liked videos
- **Format:** JSON
- **Time:** 1-4 days processing
- **Limitations:**
  - Draft videos not included
  - Sound/music metadata limited
  - No analytics export for creators

---

## Reddit

### Data Export
**Tool:** GDPR/Data Request
- **Path:** reddit.com/settings/data-request
- **Data Available:** Posts, comments, saved items, subscriptions, messages
- **Format:** CSV, JSON
- **Time:** Up to 30 days
- **Limitations:**
  - No native full export UI
  - Third-party tools needed for comprehensive backup
  - Awards/gold history not included

### Third-Party Tools
- **Reddit Data Extractor:** Python scripts
- **Pushshift API:** Historical data (limited access)

---

## YouTube

### Google Takeout
**Tool:** Google Takeout
- **URL:** https://takeout.google.com
- **Data Available:** Videos, comments, playlists, subscriptions, history
- **Format:** Various (video files, JSON metadata)
- **Limitations:**
  - Videos: original upload quality
  - Comments: text only, no threading context
  - Analytics: separate export for creators

---

## Mastodon (Fediverse)

### Native Export
**Tool:** Account export
- **Path:** Preferences → Import and export → Data export
- **Data Available:** Follows, lists, bookmarks, muted/blocked users
- **Format:** CSV
- **Limitations:**
  - NO toots export (by design - content belongs to instances)
  - Media must be downloaded separately
  - Different export per instance

### Migration
- **Account redirect:** Settings → Account → Moving to a new account
- **Followers transfer:** Supported between instances
- **Toots:** NOT transferable (ActivityPub limitation)

---

## Bluesky

### AT Protocol
**Tool:** Account data export (limited)
- **Current Status:** Basic export available
- **Data:** Posts, followers, following
- **Format:** JSON (via API)
- **Limitations:**
  - Still developing export tools
  - No official full archive download yet
  - Third-party tools emerging

---

## Research Notes

### Automation Potential
| Platform | API Available | Automation Difficulty | Notes |
|----------|--------------|----------------------|-------|
| X/Twitter | Yes (v2) | Medium | Rate limits strict |
| Reddit | Yes | Low | Pushshift alternative |
| Mastodon | Yes | Low | Instance-dependent |
| LinkedIn | Yes (restricted) | Hard | Commercial use limited |
| Facebook | Limited | Hard | Privacy restrictions |
| Instagram | Limited | Hard | Graph API complex |

### Script Ideas
1. **Cross-poster:** Mastodon ↔ Bluesky ↔ X
2. **Archive organizer:** Sort media by date, extract metadata
3. **Contact backup:** Unified address book from all platforms
4. **Message migrator:** Convert formats between platforms

---

## Useful Resources & Links

### Official Documentation
- **Meta DYI:** https://www.facebook.com/dyi
- **Instagram Data Download:** https://www.instagram.com/accounts/privacy_and_security/data/
- **X API Docs:** https://developer.x.com/en/docs/x-api
- **LinkedIn Data Export:** https://www.linkedin.com/mypreferences/d/download-my-data
- **Google Takeout:** https://takeout.google.com (YouTube)

### Third-Party Tools
- **ExportData.io:** https://www.exportdata.io — Complete X/Twitter export
- **AllMyTweets:** https://www.allmytweets.net — View all tweets
- **Reddit Data Extractor:** https://github.com/reddit-archive/reddit-data-extractor
- **Mastodon Bridge:** https://bridge.joinmastodon.org — Find Twitter friends on Mastodon

### Research & Guides
- **EFF Data Privacy:** https://www.eff.org/issues/data-privacy
- **MyData Initiative:** https://mydata.org — Data portability standards
- **Open Data Institute:** https://theodi.org — Data portability research

---

*Next Steps:*
- [ ] Test each export process with real accounts
- [ ] Document time requirements
- [ ] Create automation scripts
- [ ] Build comparison matrix

*Last Updated: 2026-02-14*
