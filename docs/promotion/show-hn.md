# Show HN Post

## Title

Show HN: No Bad Prompts – Automated prompt QA for Claude Code

## URL

https://github.com/ziweek/no-bad-prompts

## Text

I kept running into the same problem: I'd write a system prompt, test it with one or two messages, think it worked, then watch it fail on real users with different expectations.

So I built a Claude Code plugin that automates prompt testing. It extracts evaluation criteria directly from your prompt text (not a generic rubric), generates diverse test personas, runs them all in parallel, and scores each criterion with evidence from the actual responses.

The key insight: criteria derived from the prompt itself catch things generic checklists miss. "Always greet by name" becomes a testable criterion — and when persona #4 asks about a competitor, you find out whether "never recommend competitors" actually holds.

Example: a vague code review prompt ("review the code and give feedback") scored 3.0/5.0 — feedback was generic, missed security issues. After the tool rewrote it with structured sections and specificity requirements, it scored 4.7/5.0.

It's a Claude Code plugin — install and run in two lines:

```
/plugin marketplace add ziweek/no-bad-prompts
/plugin install no-bad-prompts@ziweek-no-bad-prompts
/no-bad-prompts:score-prompt "your prompt here"
```

5 commands from quick scoring to full interactive evaluation with rewrite suggestions. MIT licensed.

---

## First Comment (post immediately after submission)

Some technical details for those interested:

**How it works under the hood:**

1. **Plan** — Parses the prompt and extracts 3-7 observable, testable criteria (e.g., "Always greet by name" → Name Greeting criterion)
2. **Personas** — Generates N diverse test users designed to stress-test different aspects of the prompt
3. **Execute** — Launches parallel subagents, one per persona. Each agent receives the system prompt and the persona's request, returns raw output
4. **Evaluate** — Scores each criterion 1-5 per persona, with evidence (quoted response text)
5. **Analyze** — Determines if the prompt is "improvable" or "sufficient"
6. **Rewrite** — If improvable, generates a concrete rewrite with a change-by-change rationale

**Design decisions:**
- Criteria come from the prompt itself, not a generic rubric — this is what makes it actually useful for YOUR specific prompt
- Evidence-based scoring means every number is backed by a quote — no hand-wavy "feels like a 4"
- Parallel execution via subagents keeps evaluation fast even with many personas
- Language-agnostic: Korean prompts get Korean personas and Korean evaluation

Born from a LangGraph-based prototype I built earlier (https://github.com/ziweek/no-bad-prompts). The core concept worked well enough that I ported it to a zero-setup Claude Code plugin.

Happy to answer questions about the approach or the implementation!

---

## Posting Guide

- **Best time:** Tuesday–Thursday, 8–10 AM US Eastern (10 PM–midnight KST)
- **Post the first comment** immediately after submission
- **Stay online** for 2-3 hours after posting to respond to comments quickly
- **Tone:** Technical, humble, focused on the problem and approach — not salesy
- **If asked "why not just use X?"** — acknowledge alternatives honestly, explain what's different (criteria from prompt text, persona-based testing, parallel execution)
