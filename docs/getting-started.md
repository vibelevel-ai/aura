# Getting started

Aura runs through an **MCP server**. You connect it to the AI agent you already use,
generate a token once, and then ask your agent to score your work.

## Prerequisites

- An **MCP-capable agent** (Claude Code, Cursor, Claude Desktop, VS Code, or another MCP
  client).
- A **VibeLevel Aura account** and a **Personal Access Token** (PAT).

## 1. Generate a token

Create a Personal Access Token from your Aura account settings on the web. It looks like:

```
aura_xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
```

Treat it like a password. One token works everywhere — reuse it across your agents.
You can rename or revoke it any time from the same settings page.

## 2. Add the MCP server

Add this to your agent's MCP configuration, replacing the token:

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

> The MCP endpoint is shown in your account's "Connect your agent" card — use the value
> there if it differs.

**Client notes**

- **Claude Code / Cursor / Claude Desktop** — paste the config above into the client's
  MCP settings. These read the `Authorization` header directly.
- **VS Code** — its MCP client may open a browser login instead of reading the header;
  paste the same token there.
- **OAuth-only clients** (some marketplace connectors) — connect via the login flow and
  paste your PAT when asked.

## 3. Score a session

After you finish a real piece of work, ask your agent:

> "score this session"

Your agent builds a **redacted** summary of the session (see
[Privacy & redaction](privacy-and-redaction.md)), sends it to Aura, and returns your
score, level, archetype, and a few insight cards. Re-scoring the same session won't
double-count it.

## 4. Import your history (one-shot)

To bootstrap a rich profile from past work:

> "import my history"

Your agent reads your local session history, redacts each session, and sends them in
chunks. It's safe to run again — already-scored sessions are skipped.

## 5. Better telemetry (optional but recommended)

Scoring runs through *your own* local agent/model, so some stats depend on what your tool
exposes. For the most accurate **token / usage** numbers in Claude Code, run:

```
/context     # or /usage
```

…and your agent will fold the real counts in (marked **measured**). If your tool doesn't
expose token usage, Aura falls back to **estimated** counts — clearly labeled, and
**never used to affect your score** (see [How scoring works → Telemetry provenance](how-scoring-works.md#telemetry-provenance)).

## 6. View your profile

Open your Aura profile on the web to see your score, level, archetype, dimension
breakdown, insight cards, personal bests, and leaderboard rank. If you set a **handle**
and make your profile **public**, you get a shareable link.
