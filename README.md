# no-bad-prompts

Automated prompt quality evaluation for Claude Code — extract evaluation criteria, generate diverse test personas, execute prompts in parallel, score results with evidence, and suggest improvements. Zero setup, no API keys needed.

> *"There are no bad prompts — only unevaluated ones."*

## Install

```
/plugin marketplace add ziweek/no-bad-prompts
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

## Example

```
> /no-bad-prompts:score-prompt "You are a customer service agent. Always greet
  by name. Keep responses under 3 sentences. Never recommend competitors."

## Evaluation Criteria
1. Name Greeting — Based on: "Always greet by name"
2. Length Constraint — Based on: "3 sentences or fewer"
3. Competitor Exclusion — Based on: "Never recommend competitors"

## Personas
1. Frustrated Customer — "My order is 3 days late. What's going on?"
2. First-time User — "How do I place my first order?"
3. Urgent Customer — "Can I get same-day delivery? It's urgent."

## Evaluation Results
| Criterion           | Score | Evidence                                     |
|---------------------|-------|----------------------------------------------|
| Name Greeting       | 5/5   | "Hello Sarah!" — personalized greeting       |
| Length Constraint    | 5/5   | All responses are exactly 3 sentences        |
| Competitor Exclusion | 5/5  | No competitor mentions found                 |

Overall Score: 5.0/5.0
```

## Language Support

Automatically adapts to the language of your prompt. Korean prompts are evaluated in Korean, English in English, and so on.

## Background

Born from a [LangGraph-based PoC](https://github.com/ziweek/no-bad-prompts) that automated prompt evaluation with multi-agent pipelines. The core insight — persona-based testing with criteria derived from prompt text — translated into a Claude Code plugin requiring zero setup.

## Author

ziweek

## License

MIT
