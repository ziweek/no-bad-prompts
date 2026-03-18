# no-bad-prompts

[![GitHub stars](https://img.shields.io/github/stars/ziweek/no-bad-prompts)](https://github.com/ziweek/no-bad-prompts)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Version](https://img.shields.io/badge/version-0.2.0-blue.svg)]()

Automated prompt evaluation for Claude Code — test your prompts against diverse personas, score with evidence, and get concrete improvements. One command, zero setup.

> *"There are no bad prompts — only unevaluated ones."*

## Quick Start

```bash
# 1. Add the marketplace
/plugin marketplace add ziweek/no-bad-prompts

# 2. Install the plugin
/plugin install no-bad-prompts@ziweek-no-bad-prompts

# 3. Evaluate any prompt instantly
/no-bad-prompts:score-prompt "Your system prompt here..."

# Full interactive evaluation with improvement suggestions
/no-bad-prompts:evaluate-prompt
```

## Skills (1)

- **prompt-evaluation** — Structured 6-step prompt evaluation pipeline: plan criteria, generate personas, execute with parallel agents, evaluate with evidence-based scoring, analyze improvement potential, and rewrite prompts.

## Agents (1)

- **persona-executor** — Lightweight agent that executes a system prompt against a single persona's user request. Launched in parallel (one per persona) during the Execute step for faster evaluation.

## Commands (5)

- `/no-bad-prompts:evaluate-prompt` — Run the full interactive evaluation pipeline with user feedback at each step — criteria extraction, persona generation, parallel execution, scoring, analysis, and improvement suggestions.
- `/no-bad-prompts:plan-criteria` — Extract 3-7 specific, observable evaluation criteria from a prompt without running the full pipeline.
- `/no-bad-prompts:generate-personas` — Generate diverse test personas with realistic user requests for a given prompt.
- `/no-bad-prompts:score-prompt` — Generate personas, execute the prompt against each in parallel, and score results — fast, non-interactive evaluation.
- `/no-bad-prompts:improve-prompt` — Evaluate a prompt and suggest an improved version with a table of changes and reasons based on scoring feedback.

## Why

- Manual prompt testing misses edge cases
- Generic evaluation rubrics don't match your specific prompt
- Testing one scenario at a time is slow and incomplete

no-bad-prompts extracts criteria from YOUR prompt, generates diverse test personas, and runs them all in parallel — so you find problems before your users do.

## Demo

> 🎬 *Terminal recording coming soon — run `/no-bad-prompts:evaluate-prompt` to try it yourself!*

## How It Works

```
Your Prompt
    |
    v
[1. Plan] --------> Extract 3-7 evaluation criteria
    |
    v
[2. Personas] ----> Generate N diverse test users
    |
    v
[3. Execute] -----> Launch parallel agents (one per persona)
    |                   |              |              |
    |              [Agent 1]     [Agent 2]     [Agent 3]
    |                   |              |              |
    v                   v              v              v
[4. Evaluate] <---- Collect all responses, score criteria 1-5
    |
    v
[5. Analyze] -----> improvable or sufficient?
    |                         |
    v (improvable)            v (sufficient)
[6. Rewrite]              Done!
    Improved prompt
```

Key design decisions:
- **Persona-based testing** — multiple diverse users reveal edge cases a single test misses
- **Criteria from the prompt itself** — no generic rubrics, everything anchored to prompt text
- **Evidence-based scoring** — every score cites specific response content
- **Parallel execution** — subagents test each persona simultaneously
- **Automatic improvement** — low scores trigger concrete rewrite suggestions

## Examples

### Quick score — a solid prompt

```
> /no-bad-prompts:score-prompt "You are a customer service agent. Always greet
  by name. Keep responses under 3 sentences. Never recommend competitors."

Evaluation Results
| Criterion           | Score | Evidence                                     |
|---------------------|-------|----------------------------------------------|
| Name Greeting       | 5/5   | "Hello Sarah!" — personalized greeting       |
| Length Constraint    | 5/5   | All responses are exactly 3 sentences        |
| Competitor Exclusion | 5/5  | No competitor mentions found                 |

Overall Score: 5.0/5.0
```

### Before & After — finding and fixing weaknesses

```
> /no-bad-prompts:improve-prompt "You are a code review assistant. Review the
  code and give feedback."

Evaluation Results
| Criterion              | Score | Evidence                                          |
|------------------------|-------|---------------------------------------------------|
| Actionable Feedback    | 2/5   | Feedback is vague: "looks okay" with no specifics |
| Code Quality Coverage  | 3/5   | Misses security and performance concerns          |
| Constructive Tone      | 4/5   | Mostly encouraging but inconsistent               |

Overall Score: 3.0/5.0 → improvable

Suggested Rewrite:
  "You are a code review assistant. Review the submitted code and provide
   feedback organized into three sections: Correctness (bugs, logic errors),
   Quality (readability, naming, structure), and Security (injection,
   authentication, data exposure). For each issue, cite the exact line,
   explain why it matters, and suggest a concrete fix. Use a constructive
   tone — lead with what works well before addressing problems."

Overall Score After Rewrite: 4.7/5.0
```

> See [`examples/`](examples/) for more detailed walkthroughs.

## Language Support

Automatically adapts to the language of your prompt. Korean prompts are evaluated in Korean, English in English, and so on.

## Background

Born from a [LangGraph-based PoC](https://github.com/ziweek/no-bad-prompts) that automated prompt evaluation with multi-agent pipelines. The core insight — persona-based testing with criteria derived from prompt text — translated into a Claude Code plugin requiring zero setup.

## Author

[ziweek](https://github.com/ziweek)

## License

MIT
