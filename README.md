# Token Analysis Skill for OpenClaw

A founder-first research framework for evaluating early-stage crypto tokens. Built for [OpenClaw](https://openclaw.com) agents.

## What it does

- **6-step token analysis** — Founder deep-dive, product reality, team signal, market structure, narrative fit, and decision output
- **Watchlist management** — Track tokens with entry/exit targets, kill conditions, and running notes
- **Monitoring** — Set up cron-based price/social monitoring with alerts
- **Investment philosophy** — Portable playbook covering metagame theory, attention economics, and probabilistic thinking

## Install

Clone this repo into your agent's skills directory. Works with any agent that reads markdown skill files.

```bash
cd your-agent-workspace
git clone https://github.com/CnxLuc/token-analysis.git skills/token-analysis
```

### OpenClaw

Drop into your `skills/` directory. OpenClaw picks it up automatically from the skill description.

### Claude Code (Codex)

Add to your project's `.codex/` or reference it in your `AGENTS.md`:

```bash
git clone https://github.com/CnxLuc/token-analysis.git .codex/token-analysis
```

Then tell your agent about it — add to `AGENTS.md` or system prompt:
```
For token analysis, read .codex/token-analysis/SKILL.md
```

### OpenAI Codex

Same pattern — clone into your workspace and reference in your agent instructions:

```bash
git clone https://github.com/CnxLuc/token-analysis.git skills/token-analysis
```

### Any AI Agent

This is just markdown files. The skill works with any agent that can:
1. Read markdown instructions (`SKILL.md`)
2. Fetch URLs (DexScreener API — free, no key needed)
3. Read/write JSON (`watchlist.json`)

Clone it, point your agent at `SKILL.md`, and it'll know what to do.

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
