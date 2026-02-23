---
name: token-analysis
description: >
  Founder-first research framework for early-stage crypto tokens. 6-step analysis
  with X/Twitter + Farcaster social data, wallet verification, watchlist, and monitoring.
  Triggers: "analyze token", "should I buy", "token research", "watchlist", or any DexScreener link.
metadata:
  openclaw:
    emoji: "🔬"
---

# Token Analysis Skill

Founder-first research framework for early-stage crypto tokens. Evaluate tokens systematically, manage a watchlist, and monitor positions.

For deep analysis, read `references/playbook.md` in this skill's directory — it contains the investment philosophy (metagame lifecycle, attention theory, probabilistic thinking) that informs every evaluation.

For a completed example showing expected depth and tone, see `references/example-analysis.md`.

## Analysis Framework

**Always verify token identity by contract address + chain before analysis.** Ticker symbols are not unique — multiple tokens can share the same symbol. Use the contract address from DexScreener as the canonical identifier.

When evaluating any token, assess these in order:

### 1. Founder / Dev Deep Dive (MOST IMPORTANT)

- Find the dev/founder on **both X/Twitter and Farcaster**. Search for their recent posts, bio, follower count on each platform.
- Background: prior projects, exits, credentials.
- Social graph: who follows them? Notable backers/mutuals? Quality of engaged accounts (builders vs bots).
- Activity: posting frequency, shipping updates, engagement levels.
- **Farcaster wallet check:** if the dev has a Farcaster profile, pull their verified addresses. Do they match the deployer wallet? Are they still holding? This is a high-signal verification that X/Twitter cannot provide.
- Red flags: anonymous with no history, inactive, only posting price action, verified wallet doesn't match deployer or has sold.
- If no founder/dev can be identified, flag this as a significant risk factor. Anonymous with no history is a red flag — not a dealbreaker if product traction is strong, but requires higher conviction on other criteria.
- Always hyperlink: `[@dev](https://x.com/dev)` and `[@dev](https://warpcast.com/dev)`

### 2. Product Reality

- Does a working product exist or is it vaporware?
- Onchain activity beyond token trading?
- Users, integrations, traction metrics?

### 3. Team Signal

- Other team members, advisors, backers.
- Background (pseudonymous is fine if building; silent is not).
- Hiring? (signal of ambition and runway)

### 4. Market Structure

- FDV vs comparable projects (find the comp, calculate the gap).
- Buy/sell ratio and trend.
- Liquidity depth relative to FDV.
- Holder distribution (whales, concentration).
- Token age and price history.

### 5. Narrative Fit

- Does it ride a live narrative? (AI agents, DeFi, L2 ecosystem, etc.)
- Who's talking about it? (quality > quantity). Check **both** X/Twitter and Farcaster — compare the audiences: Farcaster skews crypto-native builders, X is broader.
- Is discourse growing or fading? Search relevant Farcaster channels for the token's chain/category.
- **Wallet-verified sentiment:** on Farcaster, check if users discussing the token actually hold it (via verified addresses). Discourse from holders is stronger signal than from spectators.

### 6. Decision Output

Always end with:
- **Verdict:** watch / small entry / conviction entry / pass
- **Entry target:** specific FDV or price
- **Kill conditions:** what makes this trade dead
- **Catalyst:** what would make you scale in

### Output Template

Use this format for every analysis:

```
## [SYMBOL] Analysis — [DATE]

**Token:** [name] ([symbol])
**Address:** [contract address](https://dexscreener.com/[chain]/[contract address])
**Chain:** [chain]
**FDV:** $[X] | **Liq:** $[X] | **Age:** [X days]

### Founder / Dev
[findings — link X accounts as [@handle](https://x.com/handle), Farcaster as [@handle](https://warpcast.com/handle)]
[wallet verification: do verified Farcaster wallets match deployer? still holding?]

### Product
[findings]

### Team
[findings — link X accounts as [@handle](https://x.com/handle), Farcaster as [@handle](https://warpcast.com/handle)]

### Market Structure
[findings — include FDV vs comps, buy/sell ratio, liq/FDV ratio, holder concentration]

### Narrative
[findings — attention state on X and Farcaster, discourse trend, who's talking, wallet-verified sentiment]

### Verdict
- **Decision:** watch / small entry / conviction entry / pass
- **Entry target:** [specific FDV or price]
- **Kill conditions:** [what makes this dead]
- **Catalyst:** [what would make you scale in]
- **Confidence:** [low / medium / high]

### Sources
- [list URLs used: DexScreener, X posts, Warpcast casts/profiles, etc.]

📎 **Full report:** [telegra.ph link]
```

This is the **summary** shown in chat. The full deep-dive is published to Telegraph (see below).

**Formatting rules:**
- **Contract addresses** must hyperlink to DexScreener: `[0x...](https://dexscreener.com/base/0x...)`
- **X/Twitter accounts** must hyperlink: `[@handle](https://x.com/handle)`
- **Farcaster accounts** must hyperlink: `[@handle](https://warpcast.com/handle)`
- Never use bare addresses or @handles without links

**Output language:** Check `OUTPUT_LANG` in `.env`. If set (e.g. `ru`, `zh`, `ja`), write the entire analysis — both the chat summary and the Telegraph article — in that language. Section headers, verdicts, scenario descriptions, everything. If `OUTPUT_LANG` is empty or not set, default to English.

### Telegraph Deep Report

Every analysis gets published to [telegra.ph](https://telegra.ph) as an expanded report. The chat output is a concise summary; the Telegraph article is the full deep-dive with additional detail.

**What the Telegraph version adds beyond the chat summary:**
- **Founder / Dev:** full bio, complete social graph breakdown, all notable followers listed, screenshot-level detail on posting patterns, complete wallet verification trace
- **Product:** detailed traction metrics, contract interaction history, user growth timeline
- **Team:** full background on every identified team member, advisory connections
- **Market Structure:** full comp table (multiple comps with FDV/liquidity/age), historical price chart description, detailed holder distribution breakdown, whale wallet analysis
- **Narrative:** full list of notable mentions with links, channel-by-channel Farcaster breakdown, X/Twitter discourse timeline, sentiment summary with holder-verification stats
- **Scenarios:** 3-5 explicit scenarios with probability estimates and expected value calculation (from playbook Rule 3)
- **Raw data:** key DexScreener metrics snapshot, relevant cast/tweet excerpts with engagement numbers

**How to publish:**

All API keys are stored in `.env` in the skill directory (see `.env.example` for the template). The `.env` file is git-ignored.

**Auto-provisioning:** If `TELEGRAPH_TOKEN` is not set in `.env`, create an account automatically before the first publish:
```bash
curl -s "https://api.telegra.ph/createAccount?short_name=TokenAnalysis&author_name=Fair&author_url=https://faircaster.xyz"
```
Save the returned `access_token` as `TELEGRAPH_TOKEN` in `.env` for reuse. No user action required — the agent handles this on first run.

**After each analysis** — convert the expanded report to Telegraph Node format and publish:
```bash
curl -s -X POST "https://api.telegra.ph/createPage" \
  -H "Content-Type: application/json" \
  -d '{
    "access_token": "'$TELEGRAPH_TOKEN'",
    "title": "SYMBOL Analysis — DATE",
    "author_name": "Fair",
    "author_url": "https://faircaster.xyz",
    "content": [NODE_ARRAY],
    "return_content": false
  }'
```

The response contains `result.url` — this is the Telegraph link to include at the end of the chat summary.

**Telegraph Node format:** content is a JSON array where each element is either a plain string or an object with `tag`, `attrs` (optional), and `children`. Supported tags: `h3`, `h4`, `p`, `a`, `strong`, `em`, `b`, `i`, `code`, `pre`, `blockquote`, `br`, `hr`, `ul`, `ol`, `li`, `figure`, `img`, `figcaption`.

Example node structure for a section:
```json
[
  {"tag": "h3", "children": ["Founder / Dev"]},
  {"tag": "p", "children": [
    "Lead dev is ",
    {"tag": "a", "attrs": {"href": "https://x.com/dev"}, "children": ["@dev"]},
    " (X) and ",
    {"tag": "a", "attrs": {"href": "https://warpcast.com/dev"}, "children": ["@dev"]},
    " (Farcaster). Full background..."
  ]},
  {"tag": "p", "children": [
    {"tag": "strong", "children": ["Wallet verification:"]},
    " Verified address 0x... matches deployer. No sells."
  ]}
]
```

**Workflow for every analysis:**
1. Run the 6-step framework, gathering all data
2. Write the concise chat summary (Output Template above)
3. Write the expanded Telegraph version with full detail
4. Publish to Telegraph via `createPage`
5. Append the Telegraph URL to the chat summary
6. Log the analysis to Google Sheets (if `GOOGLE_SHEETS_WEBHOOK` is set)

### Google Sheets Logging

Every analysis is logged as a row in a Google Sheets spreadsheet — a running journal of all evaluated tokens with verdicts and report links.

**If `GOOGLE_SHEETS_WEBHOOK` is not set in `.env`, skip this step silently.**

**One-time setup:**
1. Open your Google Sheets spreadsheet
2. Menu: Extensions → Apps Script
3. Replace the contents of `Code.gs` with the script below
4. Click Deploy → New deployment → select type "Web app"
5. Set "Execute as" → Me, "Who has access" → Anyone
6. Click Deploy, authorize when prompted
7. Copy the Web app URL → save it as `GOOGLE_SHEETS_WEBHOOK` in `.env`

**Apps Script code (paste into Code.gs):**
```javascript
function doPost(e) {
  var sheet = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();
  var data = JSON.parse(e.postData.contents);
  sheet.appendRow([
    data.date,
    data.token_address,
    data.ticker,
    data.fdv,
    data.mc,
    data.liquidity,
    data.age,
    data.founder,
    data.product,
    data.team,
    data.market_structure,
    data.narrative,
    data.verdict,
    data.full_report
  ]);
  return ContentService.createTextOutput(
    JSON.stringify({ status: "ok" })
  ).setMimeType(ContentService.MimeType.JSON);
}
```

**After each analysis, POST the results:**
```bash
curl -s -L "$GOOGLE_SHEETS_WEBHOOK" \
  -H "Content-Type: application/json" \
  -d '{
    "date": "2026-02-16",
    "token_address": "0x...",
    "ticker": "SYMBOL",
    "fdv": "$14.1M",
    "mc": "$3.66M",
    "liquidity": "$279K",
    "age": "~14 months",
    "founder": "Brief founder summary (1-2 sentences)",
    "product": "Brief product summary (1-2 sentences)",
    "team": "Brief team summary (1-2 sentences)",
    "market_structure": "Key metrics summary",
    "narrative": "Brief narrative summary (1-2 sentences)",
    "verdict": "small entry / watch / pass — confidence level",
    "full_report": "https://telegra.ph/..."
  }'
```

The `-L` flag is required — Google Apps Script returns a 302 redirect. Do **not** add `-X POST` — curl infers POST from `-d`, and `-L` correctly follows the redirect as GET to get the response.

**Field mapping:**

| JSON field | Sheet column | Content |
|-----------|-------------|---------|
| `date` | DATE | Analysis date (YYYY-MM-DD) |
| `token_address` | TOKEN ADDRESS | Contract address |
| `ticker` | TICKER | Token symbol |
| `fdv` | FDV | Fully Diluted Valuation |
| `mc` | MC | Market Cap |
| `liquidity` | LIQUIDITY | Total liquidity |
| `age` | AGE | Token age |
| `founder` | FOUNDER | 1-2 sentence summary |
| `product` | PRODUCT | 1-2 sentence summary |
| `team` | TEAM | 1-2 sentence summary |
| `market_structure` | MARKET STRUCTURE | Key metrics |
| `narrative` | NARRATIVE | 1-2 sentence summary |
| `verdict` | VERDICT | Decision + confidence |
| `full_report` | FULL REPORT | Telegraph article URL |

Summary fields (FOUNDER through NARRATIVE) should be brief — 1-2 sentences, not the full section text. Language follows `OUTPUT_LANG`.

## Data Sources

### DexScreener (primary — free, no API key)

Search by token:
```
https://api.dexscreener.com/latest/dex/search?q=SYMBOL
```

Search by address:
```
https://api.dexscreener.com/latest/dex/tokens/ADDRESS
```

Web UI: `https://dexscreener.com/search?q=SYMBOL_OR_ADDRESS`

### X/Twitter Research

Social discourse is critical for early-stage tokens. Two API providers are supported — check `TWITTER_PROVIDER` in `.env`:

- `socialdata` → **SocialData API** — pay-per-use ($0.0002/tweet), no monthly cap, 120 req/min
- `xapi` → **X API v2** — tiered plans (Basic: 10K posts/mo), official API

If `TWITTER_PROVIDER` is not set, use whichever key is available (`SOCIALDATA_API_KEY` or `X_BEARER_TOKEN`). If both are set and no provider specified, prefer SocialData.

#### Provider: SocialData (`TWITTER_PROVIDER=socialdata`)

Search for the token:
```bash
curl -s "https://api.socialdata.tools/twitter/search?query=SYMBOL" \
  -H "Authorization: Bearer $SOCIALDATA_API_KEY"
```

Search for dev activity:
```bash
curl -s "https://api.socialdata.tools/twitter/search?query=from:devhandle" \
  -H "Authorization: Bearer $SOCIALDATA_API_KEY"
```

Look up a user profile:
```bash
curl -s "https://api.socialdata.tools/twitter/user/handle" \
  -H "Authorization: Bearer $SOCIALDATA_API_KEY"
```

SocialData response uses Twitter v1-style fields: `full_text`, `user.screen_name`, `user.followers_count`, `favorite_count`, `retweet_count`, `views_count`, `tweet_created_at`. Tweets are in `tweets[]` array, pagination via `next_cursor`.

#### Provider: X API v2 (`TWITTER_PROVIDER=xapi`)

Search for the token:
```bash
curl -s "https://api.x.com/2/tweets/search/recent?query=SYMBOL%20-is:retweet&max_results=20&tweet.fields=created_at,public_metrics,author_id&expansions=author_id&user.fields=username,public_metrics" \
  -H "Authorization: Bearer $X_BEARER_TOKEN"
```

Search for dev activity:
```bash
curl -s "https://api.x.com/2/tweets/search/recent?query=from:devhandle%20-is:retweet&max_results=10&tweet.fields=created_at,public_metrics" \
  -H "Authorization: Bearer $X_BEARER_TOKEN"
```

Look up a user profile:
```bash
curl -s "https://api.x.com/2/users/by/username/handle?user.fields=description,public_metrics,created_at" \
  -H "Authorization: Bearer $X_BEARER_TOKEN"
```

X API v2 response uses: `text`, `includes.users[].username`, `public_metrics.like_count`, `public_metrics.retweet_count`, `public_metrics.impression_count`, `created_at`. Tweets are in `data[]` array, pagination via `meta.next_token`.

#### Field mapping (both providers return the same data, different field names)

| Data | SocialData | X API v2 |
|------|-----------|----------|
| Tweet text | `full_text` | `text` |
| Author handle | `user.screen_name` | `includes.users[].username` |
| Followers | `user.followers_count` | `includes.users[].public_metrics.followers_count` |
| Likes | `favorite_count` | `public_metrics.like_count` |
| Retweets | `retweet_count` | `public_metrics.retweet_count` |
| Views | `views_count` | `public_metrics.impression_count` |
| Date | `tweet_created_at` | `created_at` |

#### What to search for
- The token name/symbol — gauge discourse and sentiment
- The dev/founder handle (`from:devhandle`) — check activity and shipping
- Notable accounts mentioning the token — quality of attention

#### Fallback chain
1. Use the provider set in `TWITTER_PROVIDER`
2. If that provider's key is missing or credits are exhausted → try the other provider
3. If both unavailable → fall back to web search for recent X posts, or check the dev's public X profile directly at `https://x.com/handle`

### Farcaster Research (Neynar API)

Farcaster is a decentralized social protocol popular with crypto-native builders, founders, and DeFi developers. It adds unique signal that X/Twitter cannot provide:

- **Wallet-linked identities** — every user has verified ETH/SOL addresses, so you can check if someone discussing a token actually holds it onchain.
- **Channel organization** — crypto discussion lives in specific channels (`/degen`, `/base`, `/memecoins`, etc.), making targeted search easy.
- **Higher signal-to-noise** — onchain registration reduces bot activity; wallet links add accountability.

Requires a Neynar API key (`$NEYNAR_API_KEY`). Check `$NEYNAR_PLAN` in `.env` to determine which endpoints to use.

#### Plan routing

**Before calling any Neynar endpoint, check `NEYNAR_PLAN` in `.env`:**

- **`beginner`** (free) — use only the endpoints under "Beginner endpoints" below. For cast search and channel data, use web search or Warpcast URLs as fallback.
- **`starter`** ($9/mo) — use all endpoints below, including cast search and channel APIs.

If `NEYNAR_PLAN` is not set, default to `beginner`.

#### Beginner endpoints (free — user profiles + wallet verification)

Look up a dev/founder profile:
```bash
curl -s "https://api.neynar.com/v2/farcaster/user/by_username/?username=devhandle" \
  -H "x-api-key: $NEYNAR_API_KEY"
```

Get a user's verified wallets (returns `verified_addresses.eth_addresses` and `sol_addresses`):
```bash
curl -s "https://api.neynar.com/v2/farcaster/user/bulk?fids=FID" \
  -H "x-api-key: $NEYNAR_API_KEY"
```

Reverse lookup — find Farcaster user by wallet address:
```bash
curl -s "https://api.neynar.com/v2/farcaster/user/bulk-by-address/?addresses=0xADDRESS" \
  -H "x-api-key: $NEYNAR_API_KEY"
```

**Beginner fallbacks for cast/channel data:**
- Search Farcaster casts via web search: `site:warpcast.com SYMBOL`
- Browse a channel directly: `https://warpcast.com/~/channel/CHANNEL`
- Browse a user's casts: `https://warpcast.com/username`
- Use Pinata Hub for casts by FID (no keyword search):
  ```bash
  curl -s "https://hub.pinata.cloud/v1/castsByFid?fid=FID&pageSize=10&reverse=true"
  ```

#### Starter endpoints ($9/mo — adds cast search, channels, feeds)

All beginner endpoints, plus:

Search for token mentions:
```bash
curl -s "https://api.neynar.com/v2/farcaster/cast/search/?q=SYMBOL&limit=25&sort_type=desc_chron" \
  -H "x-api-key: $NEYNAR_API_KEY"
```

Search within a specific channel:
```bash
curl -s "https://api.neynar.com/v2/farcaster/cast/search/?q=SYMBOL&channel_id=degen&limit=25&sort_type=desc_chron" \
  -H "x-api-key: $NEYNAR_API_KEY"
```

Look up channel info (follower count, member count):
```bash
curl -s "https://api.neynar.com/v2/farcaster/channel/?id=CHANNEL_ID" \
  -H "x-api-key: $NEYNAR_API_KEY"
```

Get channel feed:
```bash
curl -s "https://api.neynar.com/v2/farcaster/feed?feed_type=filter&filter_type=channel_id&channel_id=CHANNEL&limit=25" \
  -H "x-api-key: $NEYNAR_API_KEY"
```

**What to search for:**
- The token name/symbol — gauge discourse and sentiment among crypto-native builders
- The dev/founder's Farcaster profile — activity, follower count, verified wallets, channels they post in
- Relevant channels for the token's chain/category (see table below)
- Who's discussing the token — check their follower counts and wallet verification status
- The deployer wallet address (reverse lookup) — does the dev have a Farcaster presence?

**Wallet verification (Farcaster-unique signal):**
- Fetch verified addresses of users actively discussing the token
- Cross-reference with onchain data: do they actually hold the token?
- Red flag: active promoter with no holdings = potential shill
- Green signal: dev's verified wallet matches deployer address and hasn't sold
- Use `bulk-by-address` to check if notable holders have Farcaster profiles (builder vs anon whale)

**Relevant channels:**

| Channel | Topic | When to search |
|---------|-------|---------------|
| `/degen` | DEGEN, meme culture | Memecoins, tipping tokens |
| `/base` | Base L2 ecosystem | Any Base token |
| `/memecoins` | Meme tokens | Memecoins on any chain |
| `/ethereum` | Ethereum ecosystem | L1 tokens |
| `/solana` | Solana ecosystem | Solana tokens |
| `/defi` | DeFi protocols | DeFi tokens |
| `/founders` | Startup founders | Dev/founder background check |

**If Neynar API is unavailable:** Use Pinata Hub for basic lookups (no API key needed, but no keyword search):
```bash
curl -s "https://hub.pinata.cloud/v1/castsByFid?fid=FID&pageSize=10&reverse=true"
```
Or fall back to web search, or check the dev's Warpcast profile directly at `https://warpcast.com/username`.

### Chain-Specific Gotchas

The framework is chain-agnostic, but watch for these:

- **Base / L2s:** Bridge liquidity can be thin — check if liquidity is native or bridged. Low gas means more bot activity; buy/sell ratios can be misleading.
- **Solana:** Token extensions can hide transfer fees or freeze authority. Always check mint authority and whether it's revoked. pump.fun tokens have standardized mechanics but graduation to Raydium changes the liquidity profile.
- **Ethereum L1:** Gas costs mean smaller traders are priced out — holder base skews whale-heavy. Check if the token is also deployed on L2s.
- **General:** Always verify the contract address against DexScreener. Check for honeypot indicators: can you actually sell? Is there a max transaction limit? Is the deployer wallet still holding a large share?

## Watchlist Management (Optional)

Optional persistent tracking. Skip this section if you just need one-off analysis.

Watchlist file: `watchlist.json` in the skill directory.

### Schema

```json
{
  "tokens": [
    {
      "symbol": "EXAMPLE",
      "address": "0x...",
      "chain": "base",
      "addedAt": "2026-01-15",
      "status": "watching",
      "thesis": "One-line investment thesis",
      "fdvAtAdd": 1000000,
      "entryTargets": [
        { "fdv": 500000, "note": "dip buy if thesis intact" }
      ],
      "scaleTargets": [
        { "fdv": 2000000, "condition": "user growth >1000" }
      ],
      "killConditions": [
        "dev goes quiet >3 days",
        "liquidity drops below $200K"
      ],
      "exitTargets": [
        { "fdv": 10000000, "action": "take 50% off" }
      ],
      "notes": [],
      "lastChecked": null
    }
  ]
}
```

### How to Use

These are example phrases you say to your agent — not literal CLI commands.

**Add token** — say something like "watch [token]" or "add [token] to watchlist":
1. Fetch DexScreener data (price, FDV, liquidity, age)
2. Search X/Twitter and Farcaster for the token and dev
3. Build thesis, entry targets, kill conditions
4. Add to watchlist.json

**Check watchlist** — say "check watchlist" or "watchlist status":
1. For each token with status "watching" or "entered":
   - Fetch current data from DexScreener
   - Compare to entry/exit/kill targets
   - Flag anything that hit targets
2. Output concise status table

**Analyze token** — say "analyze [token]" or paste a DexScreener link:
1. Fetch DexScreener data
2. Search X/Twitter and Farcaster for token and dev
3. Run the 6-step analysis framework above
4. Output decision with sizing recommendation

**Remove token** — say "remove [token] from watchlist":
1. Set status to "killed" or "exited" with reason
2. Keep the entry for track record (don't delete)

## Token Monitoring (Optional)

This section describes the monitoring pattern. Implementation depends on your agent platform (OpenClaw cron, scheduled tasks, etc.).

### Hourly monitoring pattern

For each monitored token, the monitoring job should:
1. Fetch DexScreener data (price, FDV, liquidity, volume, buy/sell counts)
2. Search X/Twitter for dev activity and new mentions
3. Search Farcaster for dev casts and new token mentions in relevant channels
4. Compare to previous check — flag significant moves
5. Alert on: price ±15% in 1h, dev posts major update, kill condition triggered, entry target hit, liquidity change ±20%, dev's verified wallet sells tokens

### Monitor log format

Keep a log file per token at `monitors/SYMBOL.md`:
```markdown
# SYMBOL Monitor Log
## Token Info
- Address: 0x...
- Chain: base
- Dev: @handle
- Started: YYYY-MM-DD

## Updates
### YYYY-MM-DD HH:MM UTC
- Price: $X | FDV: $X | Liq: $X
- 1h: X% | 24h: X%
- Volume 1h: $X | Buys: X | Sells: X
- Dev activity (X): [summary or "none"]
- Dev activity (Farcaster): [summary or "none"]
```

## Principles

- Express conviction through sizing, not certainty.
- A "pass" is a valid and good outcome — there are infinite opportunities.
- Always show your work: scenarios, probabilities, expected value.
- If using the watchlist, update watchlist.json after every analysis.

## Disclaimer

This skill is experimental. It provides a research framework — not financial advice.

- Outputs are indicative and have not been backtested against historical performance.
- No analysis produced by this skill should be treated as a recommendation to buy or sell any asset.
- Early-stage tokens are highly volatile and carry significant risk of total loss.
- Always do your own research. An AI agent following a framework is not a substitute for human judgment.
- The authors accept no liability for any losses incurred from acting on outputs of this skill.

---

<sub>Built by [Fair](https://faircaster.xyz)</sub>
