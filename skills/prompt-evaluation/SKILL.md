---
name: prompt-evaluation
description: "This skill should be used when the user asks to 'evaluate a prompt', 'review my prompt', 'test this prompt', 'score a prompt', 'check prompt quality', 'assess this system prompt', 'generate personas for a prompt', 'improve this prompt', 'create evaluation criteria', or wants feedback on an LLM prompt's effectiveness. Provides a 6-step evaluation pipeline: plan criteria, generate personas, execute, evaluate, analyze, and rewrite."
version: 0.2.0
---

# Prompt Quality Evaluation

## Overview

Perform structured evaluation of LLM prompts through a 6-step pipeline. Generate diverse test personas, execute the prompt against each, score results against criteria derived from the prompt itself, and suggest improvements when needed.

Core principle: **There are no bad prompts — only unevaluated ones.**

## Language Handling

Respond in the same language as the prompt being evaluated. Match the user's language naturally.

## Workflow

Commands may invoke individual steps or the full pipeline. Each step is independently addressable.

---

### Step 1: Plan — Generate Evaluation Criteria

Analyze the prompt's purpose, context, and expected output to generate precise evaluation criteria.

Principles:
1. Each criterion must reflect **concrete, observable features** derived from the prompt's purpose and structure
2. Avoid generic criteria (e.g., "response quality", "helpfulness") — every criterion must be traceable to specific prompt content
3. **Quote the prompt directly** in each criterion to anchor the evaluation
4. Generate **3-7 criteria** depending on prompt complexity
5. Each criterion must test a **single, clear judgment** — do not combine multiple aspects

Output format:
```
## Evaluation Criteria

### Criterion 1: [Name]
- Based on: "[exact quote from prompt]"
- Tests: [what specifically this criterion measures]

### Criterion 2: [Name]
...
```

---

### Step 2: Generate Personas — Create Diverse Test Users

Generate realistic personas representing different user types who would interact with this prompt. Each persona has a specific role, concern, and a natural user request.

Principles:
1. Read the system prompt and identify what situations it applies to
2. Derive diverse roles or scenarios — each persona should have a specific concern or goal (e.g., frustrated customer, first-time user, power user, edge-case requester)
3. Generate the requested number of personas (default: 3)
4. For each persona, create a **natural, specific user request** as if a real person is speaking

Output format:
```
## Personas

### Persona 1: [Name]
- **Role**: [role in context]
- **Description**: [focus, concerns, motives]
- **User Request**: "[natural, everyday language request]"

### Persona 2: [Name]
...
```

---

### Step 3: Execute — Run Prompt with Each Persona (Parallel Agents)

Launch the **persona-executor** agent for each persona in parallel. Each agent receives the system prompt and one persona's user request, then returns the response.

Process:
1. For each persona from Step 2, launch a `persona-executor` agent using the Agent tool
2. **Launch all agents in a single message** (parallel execution) — do NOT launch them sequentially
3. Pass each agent the system prompt being evaluated and the persona's user request
4. Collect all responses once agents complete
5. Present results together

Agent prompt format for each persona:
```
System prompt to execute:
[the prompt being evaluated]

Persona: [name] — [role]
User request: [the persona's generated user request]

Generate a response as if you are the LLM with this system prompt active.
```

Output format:
```
## Execution Results

### Persona 1: [Name]
**User Request**: "[request]"
**Response**:
[response from persona-executor agent]

### Persona 2: [Name]
...
```

---

### Step 4: Evaluate — Score Each Criterion

Score the execution results from Step 3 against the criteria from Step 1.

Principles:
1. Assign **1 to 5** for each criterion
2. **Quote specific sentences or expressions from the execution results** as evidence — avoid abstract assessments
3. Clearly compare the criterion against the actual result to show the basis for each score
4. Evaluate across all persona results comprehensively

Output format:
```
## Evaluation Results

| Criterion | Score | Evidence & Reason |
|-----------|-------|-------------------|
| [name] | [N]/5 | "[quote from response]" — [explanation] |
| ... | ... | ... |

**Overall Score: [average]/5.0**
```

---

### Step 5: Analyze — Determine Improvement Potential

Based on the evaluation results, classify the prompt as one of:

**`improvable`** — When:
- One or more criteria received low scores
- The prompt could be made clearer or more effective based on feedback
- The intent is good but expression or structure needs refinement

**`sufficient`** — When:
- All criteria received high scores
- The prompt is clear, purpose-appropriate, and handles user inputs well
- No meaningful improvement suggestions exist

Do not classify as `sufficient` simply because the prompt seems "good enough." Always base the judgment on the criteria scores and evidence.

Output:
```
## Analysis

**Verdict**: [improvable / sufficient]
**Reasoning**: [explanation based on scores and evidence]
```

---

### Step 6: Rewrite — Suggest Improved Prompt

Execute only when Step 5 returns `improvable`.

Principles:
1. Analyze the original prompt
2. Use evaluation scores, criteria, and reasons to identify areas for improvement
3. Propose an improved prompt with explanation of key changes
4. If the prompt's purpose is ambiguous, ask clarifying questions

Output format:
```
## Improved Prompt

### Changes Made
| Change | Reason |
|--------|--------|
| [what changed] | [why, based on evaluation feedback] |

### Improved Prompt
[the full improved prompt text]
```

---

## Step Combinations for Commands

- **Full pipeline** (`/evaluate-prompt`): Steps 1 → 2 → 3 → 4 → 5 → 6
- **Criteria only** (`/plan-criteria`): Step 1
- **Personas only** (`/generate-personas`): Step 2
- **Score** (`/score-prompt`): Steps 2 → 3 → 4
- **Improve** (`/improve-prompt`): Steps 1 → 2 → 3 → 4 → 5 → 6 (focused on Step 6 output)

## Additional Resources

### Reference Files

For detailed evaluation patterns, scoring examples, and persona generation guidance:
- **`references/evaluation-guide.md`** — Comprehensive evaluation guide with good/bad criteria examples, scoring calibration, persona examples, and improvement loop samples
