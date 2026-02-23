## 2026-02-23 — Quote API keys with special characters in .env
SocialData API key contains `|` (pipe), which bash interprets as a command pipe when `source .env` runs. Always wrap keys containing `|`, `%`, `+`, `=`, `&`, `$`, `!` in single quotes.
Rule: When adding a new key to `.env`, check for shell-special chars and quote accordingly.
