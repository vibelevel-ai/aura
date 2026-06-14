# How scoring works

Aura measures **process, not output** — *how* you collaborated with AI, not *what* you
happened to build. Two developers can ship the same feature; the one who planned,
prompted precisely, iterated, and verified is building durable skill, and Aura sees that.

This page explains the methodology at a conceptual level. The exact scoring prompts,
model, thresholds, and weights are tuned continuously and are not published here.

---

## The pipeline

```
redacted evidence  →  per-dimension scores  →  engagement-aware adjustment  →
weighted overall (0–10)  →  level band  →  insight cards + archetype
```

You send a **redacted evidence packet** (a compact, scrubbed summary — never raw code or
prompts; see [Privacy & redaction](privacy-and-redaction.md)). Aura scores each dimension
with reasoning, applies engagement-aware adjustment, computes a weighted overall score,
maps it to a level, and derives your archetype and insight cards.

---

## Dimensions

Aura scores different dimensions depending on whether the session is **coding** or
**non-coding** (your agent labels it, or Aura classifies it). Each is grouped into one of
two categories:

- **Human Effort** — what *you* brought: how you directed, steered, and reasoned.
- **Output Quality** — the quality of the result that the collaboration produced.

### Coding sessions

| Dimension | Category | What it measures |
|---|---|---|
| Prompting | Human Effort | Clarity, specificity, and iteration in how you instruct the AI |
| AI Pairing | Human Effort | Goal-setting, plan awareness, and steering the AI |
| Product Thinking | Human Effort | User perspective and validating behavior |
| Requirements Completion | Output Quality | Completeness and correctness of the solution |
| Design Thinking | Output Quality | Architecture, decomposition, engineering judgment |
| Code Understanding | Output Quality | Independent comprehension and debugging |
| Testing | Output Quality | Proactive testing and a test-driven approach |

### Non-coding sessions

| Dimension | Category | What it measures |
|---|---|---|
| Prompting | Human Effort | Clarity, context, and constraints you communicate |
| AI Collaboration | Human Effort | Steering, iterating, and course-correcting the AI |
| Strategic Thinking | Human Effort | Audience awareness, framing, and strategic depth |
| Deliverable Quality | Output Quality | Completeness and professionalism of the result |
| Structured Thinking | Output Quality | Logical structure and framework application |

> **Weighting.** Human-Effort dimensions carry the majority of the weight — Aura
> deliberately rewards *how you worked* over the raw artifact. Exact per-dimension weights
> are tuned over time.

---

## Engagement-aware adjustment

High output with **low engagement** usually means *the AI did the work*, not you. So when
a session shows thin engagement, Aura caps the Output-Quality dimensions — a genuinely
human-driven session is never penalized, but a passive one can't borrow the AI's polish.

Engagement is judged from **source-independent behavioral signals** that are always
reliable because they come straight from the session shape:

- number of your prompts (did you actually drive the session?)
- how often you redirected / corrected the AI (steering)
- tool-call count and diversity
- sub-agent / agent usage
- session duration

Token-ratio-based adjustment is applied **only when token data is *measured*** (see
below). Missing or estimated token data never lowers your score.

---

## Telemetry provenance

Aura's credibility depends on never presenting an estimate as a measured fact. Every token
stat carries one of three provenance tiers:

| Provenance | Meaning | Effect on score |
|---|---|---|
| `measured` | Exact figure from your tool's own telemetry (e.g. a `/context` or `/usage` paste) | Can inform engagement adjustment |
| `estimated` | Derived from observable session volume; approximate, always labeled | **Display only — never affects your score** |
| `unavailable` | Not even estimable, or you opted out | Shown as N/A |

Behavioral signals (prompts, redirects, tool calls) are always **counted**, never
estimated — they are the real scoring basis.

---

## Levels

The weighted overall (0–10) maps to a level band:

**Emerging → Capable → Strong → Exceptional**

You also get a **Human Contribution** meta-label that classifies your overall initiative
for the session — e.g. *Passive Delegator*, *Balanced Builder*, *Active Contributor*,
*Vibe Coder*.

---

## Archetypes

Your archetype is a behavioral cluster derived from your prompting style, pairing habits,
and tool usage (e.g. "The Vibe Coder", "The Vibe Writer"). It's a *style* signature, not a
ranking — two people at the same score can have very different archetypes.

---

## Insight cards & nudges

Each session produces **cards** — a question, a punchy answer, and one stat — at two
levels: per-session and overall (aggregated across your sessions). Cards come in two
classes:

- **Credibility cards** — steering, planning, verification habits.
- **Personality cards** — your go-to phrase, prompt length, signature move (the
  shareable, fun ones).

Many cards carry a **growth nudge**: one specific, actionable thing to try next session.

---

## What Aura does *not* do

- It does **not** read or store your code, or score it against a standard you didn't agree
  to.
- It does **not** rank you against other people by default — your data is yours; public
  surfaces (leaderboard, shared profile) are opt-in.
- It measures **how you work**, which is durable and portable — independent of what you
  happened to be building.
