---
name: token-analysis
description: >
  Token analysis, watchlist management, and monitoring for early-stage crypto tokens.
  Founder-first research framework with 6-step evaluation. Use when asked to:
  analyze a token, do token analysis, evaluate a token, research a token,
  "should I buy", watch a token, add/check/remove watchlist, token research,
  or when given a DexScreener link.
metadata:
  openclaw:
    emoji: "🔬"
---

# Token Analysis Skill

Founder-first research framework for early-stage crypto tokens. Evaluate tokens systematically, manage a watchlist, and monitor positions.

For deep analysis, read `references/playbook.md` in this skill's directory — it contains the investment philosophy (metagame lifecycle, attention theory, probabilistic thinking) that informs every evaluation.

## Analysis Framework

**Always verify token identity by contract address + chain before analysis.** Ticker symbols are not unique — multiple tokens can share the same symbol. Use the contract address from DexScreener as the canonical identifier.

When evaluating any token, assess these in order:

### 1. Founder / Dev Deep Dive (MOST IMPORTANT)

- Find the dev/founder's X/Twitter account. Search for their recent tweets, bio, follower count.
- Background: prior projects, exits, credentials.
- Social graph: who follows them? Notable backers/mutuals? Quality of engaged accounts (builders vs bots).
- Activity: posting frequency, shipping updates, engagement levels.
- Red flags: anonymous with no history, inactive, only posting price action.
- If no founder/dev can be identified, flag this as a significant risk factor. Anonymous with no history is a red flag — not a dealbreaker if product traction is strong, but requires higher conviction on other criteria.
- Always hyperlink: `[@dev](https://x.com/dev)`

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
- Who's talking about it? (quality > quantity)
- Is discourse growing or fading?

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
**Address:** [contract address]
**Chain:** [chain]
**FDV:** $[X] | **Liq:** $[X] | **Age:** [X days]

### Founder / Dev
[findings]

### Product
[findings]

### Team
[findings]

### Market Structure
[findings — include FDV vs comps, buy/sell ratio, liq/FDV ratio, holder concentration]

### Narrative
[findings — attention state, discourse trend, who's talking]

### Verdict
- **Decision:** watch / small entry / conviction entry / pass
- **Entry target:** [specific FDV or price]
- **Kill conditions:** [what makes this dead]
- **Catalyst:** [what would make you scale in]
- **Confidence:** [low / medium / high]

### Sources
- [list URLs used: DexScreener, X posts, etc.]
```

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

Search X/Twitter for:
- The token name/symbol — gauge discourse and sentiment
- The dev/founder handle (`from:devhandle`) — check activity and shipping
- Notable accounts mentioning the token

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
2. Search X/Twitter for the token and dev
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
2. Search X/Twitter for token and dev
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
3. Compare to previous check — flag significant moves
4. Alert on: price ±15% in 1h, dev posts major update, kill condition triggered, entry target hit, liquidity change ±20%

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
- Dev activity: [summary or "none"]
```

## Principles

- Express conviction through sizing, not certainty.
- A "pass" is a valid and good outcome — there are infinite opportunities.
- Always show your work: scenarios, probabilities, expected value.
- If using the watchlist, update watchlist.json after every analysis.

---

<sub>Built by [Fair](https://faircaster.xyz)</sub>
