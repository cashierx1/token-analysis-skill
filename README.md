# Token Analysis

A founder-first research framework for evaluating early-stage crypto tokens. Teach your AI agent how to do proper token research.

Works with [OpenClaw](https://openclaw.com), [Claude Code](https://docs.anthropic.com/en/docs/agents-and-tools/claude-code/overview), [Codex](https://openai.com/index/codex/), or any agent that can read markdown.

## What it does

- **6-step token analysis** — Founder deep-dive, product reality, team signal, market structure, narrative fit, and decision output
- **Investment philosophy** — Portable playbook covering metagame theory, attention economics, and probabilistic thinking
- **Watchlist** (optional) — Track tokens with entry/exit targets, kill conditions, and running notes
- **Monitoring** (optional) — Set up cron-based price/social monitoring with alerts

The core skill is the analysis framework. The watchlist and monitoring are optional add-ons if your agent needs to track positions over time.

## Install

Clone this repo into your agent's workspace:

```bash
git clone https://github.com/CnxLuc/token-analysis.git
```

### OpenClaw

Drop into your `skills/` directory. It gets picked up automatically.

```bash
git clone https://github.com/CnxLuc/token-analysis.git skills/token-analysis
```

### Claude Code

Clone into your project and reference it in `AGENTS.md` or your system prompt:

```bash
git clone https://github.com/CnxLuc/token-analysis.git .claude/token-analysis
```

```
For token analysis, read .claude/token-analysis/SKILL.md
```

### Codex

Clone into your workspace and reference in your agent instructions:

```bash
git clone https://github.com/CnxLuc/token-analysis.git .codex/token-analysis
```

### Any AI Agent

This is just markdown files. It works with any agent that can:
1. Read markdown instructions (`SKILL.md`)
2. Fetch URLs (DexScreener API — free, no key needed)
3. Optionally read/write JSON (for the watchlist feature)

Point your agent at `SKILL.md` and it'll know what to do.

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
