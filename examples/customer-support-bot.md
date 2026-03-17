# Example: Customer Support Bot

## Prompt

```
You are a customer service agent. Always greet by name. Keep responses under
3 sentences. Never recommend competitors.
```

## Command

```
/no-bad-prompts:evaluate-prompt
```

## Step 1 — Criteria Extraction

| # | Criterion           | Based on                       |
|---|---------------------|--------------------------------|
| 1 | Name Greeting       | "Always greet by name"         |
| 2 | Length Constraint    | "Keep responses under 3 sentences" |
| 3 | Competitor Exclusion | "Never recommend competitors" |

## Step 2 — Personas

| # | Persona             | Request                                      |
|---|---------------------|----------------------------------------------|
| 1 | Frustrated Customer | "My order is 3 days late. What's going on?"  |
| 2 | First-time User     | "How do I place my first order?"             |
| 3 | Urgent Customer     | "Can I get same-day delivery? It's urgent."  |
| 4 | Competitor Asker    | "Is ProductX better than yours for my case?" |

## Step 3 — Execution

Each persona is run in parallel via the `persona-executor` agent. Four agents launch simultaneously — one per persona.

## Step 4 — Evaluation

| Criterion           | Persona 1 | Persona 2 | Persona 3 | Persona 4 | Avg   |
|---------------------|-----------|-----------|-----------|-----------|-------|
| Name Greeting       | 5/5       | 5/5       | 5/5       | 5/5       | 5.0   |
| Length Constraint    | 5/5       | 5/5       | 5/5       | 5/5       | 5.0   |
| Competitor Exclusion | 5/5      | 5/5       | 5/5       | 5/5       | 5.0   |

**Overall Score: 5.0/5.0**

## Step 5 — Analysis

**Verdict: sufficient**

All criteria are met consistently across all personas, including the edge case where a user directly asks about a competitor. The prompt's constraints are clear and specific enough to produce reliable behavior.

## Takeaway

This prompt works well because each instruction is concrete and testable. "Always greet by name" and "under 3 sentences" leave no room for ambiguity. Well-written constraints lead to high evaluation scores.
