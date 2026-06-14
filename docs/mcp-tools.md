# MCP tools

The Aura MCP server exposes a small set of agent-facing tools. You don't call these
directly — you ask your agent in plain language ("score this session", "what's my Aura?")
and it picks the right tool. This page documents what each does.

All tools resolve **who you are** from your Personal Access Token — no user id is ever
passed in.

| Tool | Ask your agent… | What it does |
|---|---|---|
| `score_this_session` | "score this session" | Scores ONE just-finished session from a redacted evidence packet; returns score, level, archetype, dimension scores, and session cards. Idempotent — re-scoring won't double-count. |
| `import_history` | "import my history" | Bulk-imports your past sessions (in chunks) to bootstrap a rich profile. Safe to re-run; already-scored sessions are skipped. |
| `get_my_profile` | "what's my Aura?" / "show my profile" | Returns your aggregate profile: overall score, level, archetype, averaged dimensions, overall cards, recent sessions, and stats. |
| `compare_me` | "how do I rank?" | Returns how you compare to your cohort (percentile / rank). **Note:** `percentile` and `rank` currently return `null` — cohort ranking is a Phase-2 feature, not yet built. |
| `whoami` | "is Aura connected?" | Confirms the connection and which account is linked; returns a link to your profile. Carries no scores. |

## Inputs & outputs (high level)

- **`score_this_session(evidence)`** — `evidence` is the redacted
  [evidence packet](privacy-and-redaction.md#the-evidence-packet-public-contract).
  Returns `aura_score` (0–10), `aura_level`, `archetype`, `dimension_scores`
  (score + reasoning per dimension), `cards`, a human-contribution label, and a
  `profile_delta` showing how this session moved your running Aura.

- **`import_history(sessions)`** — a list of redacted evidence packets (same shape).
  Returns counts: `scored`, `skipped` (deduped), `total`. Send in chunks; a failed chunk
  is safe to resubmit.

- **`get_my_profile()`** / **`whoami()`** / **`compare_me()`** — no arguments; resolved
  from your token. Note that `compare_me()` currently returns `null` for `percentile`
  and `rank` — cohort ranking is a Phase-2 feature, not yet built.

## Notes

- The evidence shape is the **public redaction contract** — raw transcripts never need to
  be sent. See [Privacy & redaction](privacy-and-redaction.md).
- Tools are stateless and idempotent where it matters (dedup by a per-session
  fingerprint), so retries and re-imports are safe.
