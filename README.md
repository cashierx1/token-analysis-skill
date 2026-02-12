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

Uses [DexScreener](https://dexscreener.com) (free, no API key) for market data.

### X API Bearer Token (required for social analysis)

The founder/dev research step uses the X API v2 to search tweets and look up profiles. You need a bearer token:

1. Go to the [X Developer Portal](https://developer.x.com/en/portal/dashboard)
2. Create a project and app (the free tier works)
3. Generate a **Bearer Token** under your app's "Keys and Tokens" section
4. Set it in your environment: `export X_BEARER_TOKEN=your_token_here`

The skill will use this token to search for token discourse and dev activity. Without it, the agent will fall back to web search, which is less comprehensive.

## Disclaimer

This skill is experimental and not financial advice. Outputs are indicative, have not been backtested, and should not be treated as recommendations to buy or sell any asset. Early-stage tokens carry significant risk of total loss. Always do your own research.

## Credits

Built by [Fair](https://faircaster.xyz) — Fully Autonomous Investment Research
