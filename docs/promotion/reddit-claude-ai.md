# r/ClaudeAI Post

## Title

[Plugin] I built a prompt evaluation tool for Claude Code — it tests your prompts against diverse personas and scores them automatically

## Body

I've been using Claude Code a lot for building AI-powered features, and I kept hitting the same wall: writing a system prompt, testing it with a couple of messages, thinking it works, then finding edge cases in production.

So I built **no-bad-prompts** — a Claude Code plugin that automates prompt testing.

**What it does:**

You give it a system prompt, and it:
1. Extracts testable criteria from the prompt itself (not a generic checklist)
2. Generates diverse test personas (frustrated customer, first-time user, edge case asker, etc.)
3. Runs the prompt against each persona in parallel
4. Scores every criterion with evidence from actual responses
5. Tells you if the prompt needs improvement, and if so, rewrites it

**Quick example:**

I tested a code review assistant prompt: *"Review the code and give feedback."*

It scored 3.0/5.0 — the feedback was vague, missed security issues, and the tone was inconsistent. The tool rewrote it with structured sections (Correctness, Quality, Security), specific instructions to cite lines and suggest fixes, and a constructive-tone-first approach. Re-evaluated at 4.7/5.0.

**Install in Claude Code:**

```
/plugin marketplace add ziweek/no-bad-prompts
/plugin install no-bad-prompts@ziweek-no-bad-prompts
```

Then run any of these:
- `/no-bad-prompts:score-prompt "your prompt"` — fast evaluation
- `/no-bad-prompts:evaluate-prompt` — full interactive pipeline
- `/no-bad-prompts:improve-prompt` — evaluation + rewrite

It's MIT licensed and works with any language (Korean, English, etc.).

GitHub: https://github.com/ziweek/no-bad-prompts

Would love feedback from other Claude Code users — what prompts would you want to test with this?

---

## Posting Guide

- **Flair:** Use "Tool/Plugin" or "Resource" flair if available
- **Timing:** 1-2 days after Show HN post
- **Respond** to every comment, especially questions about how it works
- **Don't** cross-post the exact same text anywhere else
