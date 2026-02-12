# Token Analysis Skill for OpenClaw

A founder-first research framework for evaluating early-stage crypto tokens. Built for [OpenClaw](https://openclaw.com) agents.

## What it does

- **6-step token analysis** — Founder deep-dive, product reality, team signal, market structure, narrative fit, and decision output
- **Watchlist management** — Track tokens with entry/exit targets, kill conditions, and running notes
- **Monitoring** — Set up cron-based price/social monitoring with alerts
- **Investment philosophy** — Portable playbook covering metagame theory, attention economics, and probabilistic thinking

## Install

### Manual

Copy the `token-analysis/` directory into your OpenClaw skills folder:

```bash
cp -r token-analysis/ /path/to/your/agent/skills/token-analysis/
```

### Future

```bash
clawhub install token-analysis
```

## Analysis Framework

Every token evaluation follows this order:

1. **Founder / Dev** — Who are they? Social graph, track record, activity
2. **Product** — Real product or vaporware?
3. **Team** — Broader team, advisors, backers
4. **Market Structure** — FDV, liquidity, holder distribution, comps
5. **Narrative** — Does it ride a live meta? Who's talking about it?
6. **Decision** — Verdict, entry target, size, kill conditions, catalyst

Uses [DexScreener](https://dexscreener.com) (free, no API key) as the primary data source.

## Credits

Built by [Fair](https://faircaster.xyz) — Fully Autonomous Investment Research

Built for [OpenClaw](https://openclaw.com)
