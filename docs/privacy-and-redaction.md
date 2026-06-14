# Privacy & redaction

Aura is built so that **your raw code and prompts never leave your machine.** Your own
local agent does the reading and redaction; only a compact, scrubbed summary is sent. This
page is the published **redaction contract** — the exact shape of what crosses the wire.

## The promise

- **Raw transcripts, full prompts, and file contents never leave your machine.**
- What Aura receives is a **redacted evidence packet**: truncated excerpts, file *paths*
  and metadata (no contents), and counts/stats.
- Your agent builds it locally and can **show you the packet before sending** so you can
  approve, edit, or cancel.
- **Stateless** — there's no background collection and no stored raw transcript.

## What is sent vs. what is not

| Sent (redacted) | Never sent |
|---|---|
| Short, truncated text excerpts | Full prompts / responses / transcripts |
| File **paths** + language + size + op (created/edited/read) | File **contents** / code / diffs |
| Counts: prompts, tool calls, sub-agents, tools used | Secrets, tokens, credentials |
| Coarse timing and the model name | Anything you don't approve in the preview |
| Optional measured token totals (if you provide them) | — |

## The evidence packet (public contract)

This is the shape your agent sends. Every field is optional except `source`; excerpts are
truncated and `files_touched` carries metadata only.

```jsonc
{
  "source": "claude_code | cursor | codex | windsurf | gemini_cli | vscode | claude_desktop | claude_ai | chatgpt | perplexity | web",
  "modality": "coding | noncoding",        // optional; Aura classifies if omitted
  "title": "short human label",            // optional
  "started_at": "ISO-8601",                // optional
  "ended_at": "ISO-8601",                  // optional
  "model": "the primary model used",       // optional
  "task_type": "debugging | architecture | feature_build | code_review | writing | research | infrastructure | other", // optional

  "turns": [
    {
      "role": "user | assistant | tool",
      "text_excerpt": "TRUNCATED / redacted snippet — NOT the full message",
      "ts": "ISO-8601",
      "token_est": 123,
      "tool_name": "Edit"
    }
  ],

  "files_touched": [
    { "path": "relative/or/basename", "lang": "python", "bytes": 1024, "ops": "edited" }
    // path + metadata ONLY — no file contents
  ],

  "local_stats": {
    "tokens": { "total": 1250000, "human": 8000, "measured": true },
    "tools_used": { "Edit": 42, "Read": 30 },
    "subagent_count": 12,
    "skills_used": ["/code-review"],
    "plan_mode": false
  }
}
```

### Redaction rules your agent follows

- **Truncate** every `text_excerpt`; never send a full message.
- **Strip** secrets, tokens, keys, and credentials.
- **Abstract** proprietary names, client/customer identities, and anything sensitive — a
  short summary should convey *what kind* of work happened, not the confidential details.
- `files_touched` is **paths + metadata only** — never contents.

## Provenance: measured vs. estimated

Token stats are tagged `measured`, `estimated`, or `unavailable`. **Estimated values are
display-only and never affect your score.** For exact numbers, paste a `/context` or
`/usage` output (Claude Code) so your agent can mark them `measured`. See
[How scoring works → Telemetry provenance](how-scoring-works.md#telemetry-provenance).

## Visibility

Your profile is **private by default**. Going public (a shareable `/u/<handle>` link and
leaderboard appearance) is opt-in, and even then only scores, cards, and archetype are
shown — never your raw work. Shared session links use a generic, non-revealing label
(e.g. "An evening build session") derived only from modality + time-of-day, so a link
never leaks what the work actually was.
