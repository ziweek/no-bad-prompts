# Example: Code Review Assistant (Before & After)

## Original Prompt

```
You are a code review assistant. Review the code and give feedback.
```

## Command

```
/no-bad-prompts:improve-prompt
```

## Step 1 — Criteria Extraction

| # | Criterion              | Based on                         |
|---|------------------------|----------------------------------|
| 1 | Actionable Feedback    | "give feedback" implies useful, specific advice |
| 2 | Code Quality Coverage  | "review the code" implies comprehensive analysis |
| 3 | Constructive Tone      | "assistant" role implies helpfulness |

Note: The criteria are intentionally inferred from vague instructions — this is where under-specified prompts reveal their weakness.

## Step 2 — Personas

| # | Persona              | Request                                              |
|---|----------------------|------------------------------------------------------|
| 1 | Junior Developer     | Submits a Python function with a subtle off-by-one error |
| 2 | Security Engineer    | Submits an API endpoint with SQL injection vulnerability |
| 3 | Senior Refactorer    | Submits working but deeply nested callback code      |
| 4 | Student              | Submits a first attempt at a sorting algorithm       |

## Step 4 — Evaluation

| Criterion              | P1  | P2  | P3  | P4  | Avg  |
|------------------------|-----|-----|-----|-----|------|
| Actionable Feedback    | 2/5 | 2/5 | 3/5 | 2/5 | 2.3  |
| Code Quality Coverage  | 3/5 | 2/5 | 3/5 | 4/5 | 3.0  |
| Constructive Tone      | 4/5 | 3/5 | 4/5 | 5/5 | 4.0  |

**Overall Score: 3.1/5.0**

### Evidence Highlights

- **Actionable Feedback (2/5, Persona 1):** Response says "looks mostly fine, maybe check your loop" — no line reference, no explanation of the actual bug.
- **Code Quality Coverage (2/5, Persona 2):** Misses the SQL injection entirely. Only comments on variable naming.
- **Constructive Tone (3/5, Persona 2):** Blunt phrasing: "This code has problems" without leading with positives.

## Step 5 — Analysis

**Verdict: improvable**

The prompt is too vague. "Review the code" doesn't specify what to look for. "Give feedback" doesn't define what good feedback looks like. The assistant defaults to surface-level observations and misses critical issues.

## Step 6 — Rewrite

```
You are a code review assistant. Review the submitted code and provide
feedback organized into three sections:

1. **Correctness** — bugs, logic errors, edge cases
2. **Quality** — readability, naming, structure, duplication
3. **Security** — injection, authentication, data exposure

For each issue found:
- Cite the exact line or block
- Explain why it matters
- Suggest a concrete fix

Use a constructive tone — lead with what works well before addressing
problems. If the code is clean, say so and explain why.
```

### Re-evaluation After Rewrite

| Criterion              | P1  | P2  | P3  | P4  | Avg  |
|------------------------|-----|-----|-----|-----|------|
| Actionable Feedback    | 5/5 | 5/5 | 4/5 | 5/5 | 4.8  |
| Code Quality Coverage  | 5/5 | 5/5 | 4/5 | 4/5 | 4.5  |
| Constructive Tone      | 5/5 | 5/5 | 5/5 | 5/5 | 5.0  |

**Overall Score: 4.8/5.0** (was 3.1)

## Takeaway

Vague prompts produce vague results. Adding structure (sections), specificity (what to look for), and format (cite lines, explain, suggest) turned a mediocre prompt into a reliable one. The 1.7-point improvement shows how much clarity matters.
