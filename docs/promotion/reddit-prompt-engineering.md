# r/PromptEngineering Post

## Title

I automated prompt testing with persona-based evaluation — here's the approach and what I learned

## Body

I've been thinking a lot about how we test prompts. Most of us do something like: write a prompt, try a few messages, tweak, repeat. It works, but it's slow and biased toward the scenarios we can think of.

I wanted something more systematic, so I built an automated evaluation pipeline. Here's the approach:

### The core idea: test prompts like you test software

Instead of one person manually checking outputs, the system:

1. **Extracts criteria from the prompt itself.** If your prompt says "always greet by name" and "keep responses under 3 sentences," those become testable criteria — not a generic rubric.

2. **Generates diverse personas.** A frustrated customer, a first-time user, someone asking about a competitor, a non-native speaker. Each persona is designed to stress-test a different aspect of the prompt.

3. **Runs all personas in parallel.** Each gets the system prompt and sends their realistic request. You get raw responses for every scenario.

4. **Scores with evidence.** Every criterion gets a 1-5 score per persona, backed by a quote from the actual response. No subjective "feels like a 4."

5. **Decides and rewrites.** If the overall score is below threshold, it generates a concrete rewrite with a change-by-change rationale.

### What I learned

- **Vague prompts produce vague results** (obvious in hindsight). A code review prompt that says "give feedback" scored 3.0/5.0. Adding structure (sections for Correctness, Quality, Security) and specificity (cite lines, explain why, suggest fixes) pushed it to 4.7.

- **Persona diversity matters more than persona count.** 4 well-chosen personas catch more issues than 10 similar ones.

- **Criteria from the prompt text > generic rubrics.** When the criteria are anchored to what the prompt actually says, the evaluation catches real failures instead of theoretical ones.

- **The "before and after" is the most useful output.** Knowing a prompt scores 3.0 isn't as useful as seeing exactly which criteria failed and getting a rewrite that addresses each weakness.

### The tool

I packaged this into an open-source Claude Code plugin called **no-bad-prompts**. It runs the full pipeline in one command. Not trying to hard-sell it — I'm more interested in whether this evaluation approach resonates with how others think about prompt QA.

GitHub: https://github.com/ziweek/no-bad-prompts

**What's your current process for testing prompts?** I'm curious if others have found different approaches that work well.

---

## Posting Guide

- **Timing:** 2-3 days after r/ClaudeAI post
- **Tone:** Educational, sharing learnings — the tool is secondary to the methodology
- **Key difference from r/ClaudeAI post:** This is about the *approach*, not the *plugin*
- **End with a question** to encourage discussion
- **Respond** thoughtfully to methodology discussions — this audience cares about the "why"
