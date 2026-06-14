# VibeLevel Aura

**Your AI style. Your AI signature. Made measurable.**

Aura scores *how well you work with AI* — not what you shipped, but how you prompted,
steered, planned, and verified to get there. It works through a single **MCP server**
your AI agent already speaks to: your agent reads its own session, redacts it to a
compact summary, and sends that up. A session scores in seconds. No Docker, no daemon,
no repo mounting.

This repository is the **public documentation** for Aura — how to use it, how scoring
works, and what does (and doesn't) leave your machine. 

---

## Quickstart (60 seconds)

1. **Get a token.** Create a Personal Access Token in your VibeLevel Aura account
   settings (it looks like `aura_…`). [→ Getting started](docs/getting-started.md)
2. **Add the MCP server** to your agent (Claude Code, Cursor, Claude Desktop, VS Code,
   or any MCP client):

   ```json
   {
     "mcpServers": {
       "vibelevel-aura": {
         "type": "http",
         "url": "https://aura-mcp.vibelevel.ai/mcp",
         "headers": { "Authorization": "Bearer aura_YOUR_TOKEN_HERE" }
       }
     }
   }
   ```

3. **Score.** After a real piece of work, just say:
   > "score this session"

   Or bootstrap a rich profile from your past work:
   > "import my history"

That's it. Your Aura profile grows from there.

---

## What you get

- ✅ **Coding *and* non-coding** sessions — most tools are coding-only.
- ✅ **Any MCP client** — Claude, ChatGPT, Perplexity, Cursor, Claude Desktop, VS Code.
- 🔒 **Redacted by design** — your raw code and prompts never leave your machine.
  [→ Privacy & redaction](docs/privacy-and-redaction.md)
- 📈 **Nudge cards** — one specific thing to improve next session.
- 🏅 **Personal bests, archetypes, a shareable profile, and a public leaderboard.**

---

## Documentation

| Doc | What's in it |
|---|---|
| [Getting started](docs/getting-started.md) | Install per client, get a token, first score, history import |
| [How scoring works](docs/how-scoring-works.md) | Dimensions, levels, engagement, telemetry provenance, archetypes, cards |
| [Privacy & redaction](docs/privacy-and-redaction.md) | The published evidence contract — what leaves your machine and what never does |
| [MCP tools](docs/mcp-tools.md) | The agent-facing tools and what they return |
| [FAQ](docs/faq.md) | Common questions |

---

## Build a plugin

Want richer, automatic telemetry for your favorite agent? Plugins are community-built
local collectors that gather more accurate session data and call the Aura MCP for you.
See the **[Aura Plugins](https://github.com/vibelevel-ai/aura-plugins)** repo — contributions
welcome.

---

## Status

Aura is in **beta**. Docs here track the current behavior and will evolve. Found
something inaccurate? Open an issue.

**Community:** join us on [Discord](https://discord.gg/fBbrDJDt).

## License

[MIT](LICENSE) © 2026 VibeLevel.
