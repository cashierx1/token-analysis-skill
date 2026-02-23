# Token Analysis

A founder-first research framework for evaluating early-stage crypto tokens. Teach your AI agent how to do proper token research.

Works with [Claude Code](https://docs.anthropic.com/en/docs/agents-and-tools/claude-code/overview), [Codex](https://openai.com/index/codex/), [OpenClaw](https://openclaw.com), or any AI coding agent.

## What it does

- **6-step token analysis** — Founder deep-dive, product reality, team signal, market structure, narrative fit, and decision output
- **Investment philosophy** — Portable playbook covering metagame theory, attention economics, and probabilistic thinking
- **Watchlist** (optional) — Track tokens with entry/exit targets, kill conditions, and running notes
- **Monitoring** (optional) — Set up cron-based price/social monitoring with alerts

The core skill is the analysis framework. The watchlist and monitoring are optional if your agent needs to track positions over time.

## Install

Give your agent this repo URL and ask it to install the skill:

```
https://github.com/CnxLuc/token-analysis-skill
```

That's it. Claude Code, Codex, OpenClaw, or any coding agent will know what to do.

## Quick Start

After installing, try these prompts:

- "Analyze this token: 0x..." (paste any contract address)
- "What do you think of [TOKEN] on Base?"
- "Add [TOKEN] to watchlist" (if using optional watchlist)

## Analysis Framework

Every token evaluation follows this order:

1. **Founder / Dev** — Who are they? Social graph, track record, activity
2. **Product** — Real product or vaporware?
3. **Team** — Broader team, advisors, backers
4. **Market Structure** — FDV, liquidity, holder distribution, comps
5. **Narrative** — Does it ride a live meta? Who's talking about it?
6. **Decision** — Verdict, entry target, size, kill conditions, catalyst

Uses [DexScreener](https://dexscreener.com) (free, no API key) for market data, [X/Twitter](https://x.com) and [Farcaster](https://warpcast.com) for social research.

### API Keys Setup

All keys are **optional** — the agent falls back to web search when a key is missing.

1. Copy the template: `cp .env.example .env`
2. Fill in the keys you have (see below)
3. Load them: `source .env` or `export $(cat .env | grep -v '^#' | xargs)`

The `.env` file is git-ignored and never committed.

| Key | Service | How to get |
|-----|---------|-----------|
| `TWITTER_PROVIDER` | Twitter data source selector | `socialdata` or `xapi` (see SKILL.md) |
| `SOCIALDATA_API_KEY` | SocialData — alternative Twitter data (pay-per-use) | [socialdata.tools](https://socialdata.tools) → sign up → API key |
| `X_BEARER_TOKEN` | X/Twitter API v2 — social discourse, dev activity | [X Developer Portal](https://developer.x.com/en/portal/dashboard) → create app → Bearer Token |
| `NEYNAR_API_KEY` | Farcaster / Neynar — user profiles + wallet verification (free: 200K credits). Cast search requires Starter $9/mo | [dev.neynar.com](https://dev.neynar.com/) → create app → API key |
| `TELEGRAPH_TOKEN` | Telegraph — deep report publishing | One-time: `curl -s "https://api.telegra.ph/createAccount?short_name=TokenAnalysis&author_name=Fair&author_url=https://faircaster.xyz"` → copy `access_token` |
| `GOOGLE_SHEETS_WEBHOOK` | Google Sheets — analysis log | Extensions → Apps Script → deploy as Web App (see SKILL.md) |

## Disclaimer

This skill is experimental and not financial advice. Outputs are indicative, have not been backtested, and should not be treated as recommendations to buy or sell any asset. Early-stage tokens carry significant risk of total loss. Always do your own research.

## Credits

Built by [Fair](https://faircaster.xyz) — Fully Autonomous Investment Research
