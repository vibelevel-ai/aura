# FAQ

### What is Aura, in one line?
A score for *how well you work with AI* — prompting, steering, planning, verifying —
delivered through an MCP server your agent already speaks to.

### Do you read my code?
No. Your raw code, prompts, and file contents never leave your machine. Your local agent
sends a redacted summary (truncated excerpts, file paths + metadata, counts). See
[Privacy & redaction](privacy-and-redaction.md).

### How is this different from Docker-based tools?
There's nothing to install and run locally — no container, no daemon, no repo mounting.
Aura is just an MCP server; your agent does the gathering and redaction inline and scores
a session in seconds. It also covers **non-coding** work and works with **any MCP client**.

### Which agents/tools work?
Any MCP-capable client — Claude Code, Cursor, Claude Desktop, VS Code — plus connector-style
clients (ChatGPT, Perplexity, Claude). Telemetry richness varies by tool; see
[How scoring works → Telemetry provenance](how-scoring-works.md#telemetry-provenance).

### Why are my token stats "estimated"?
Some tools don't expose token usage programmatically, so your agent estimates it from
session volume. Estimates are labeled and **never affect your score**. For exact numbers
in Claude Code, paste a `/context` or `/usage` output.

### Will scoring the same session twice double-count it?
No. Sessions are deduplicated by a per-session fingerprint, so re-scoring and re-importing
are safe.

### Is my profile public?
Private by default. Going public (a shareable `/u/<handle>` link + leaderboard) is opt-in,
and only scores, cards, and archetype are shown — never your raw work.

### Coding only?
No — Aura scores **coding and non-coding** sessions, with dimensions tuned to each.

### Can I score my whole history?
Yes — ask your agent to "import my history". It reads your local sessions, redacts them,
and uploads in chunks. Safe to re-run.

### Can I build richer/automatic collection for my tool?
Yes — that's what plugins are for. See the
**[Aura Plugins](https://github.com/vibelevel-ai/aura-plugins)** repo and contribute.

### How do I get a token?
From your VibeLevel Aura account settings on the web. It looks like `aura_…`. One token
works across all your agents; rename/revoke any time.
