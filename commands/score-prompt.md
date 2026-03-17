---
description: "Score a prompt by generating personas, executing the prompt, and evaluating results against criteria"
argument-hint: "<prompt text or file path>"
---

# /score-prompt -- Execute and Score a Prompt

Generate test personas, run the prompt against each, and score the results against evaluation criteria.

## Invocation

```
/score-prompt "You are a helpful assistant that summarizes articles in 3 bullet points."
/score-prompt prompts/translation-prompt.txt
/score-prompt                                       # asks for the prompt
```

## Workflow

### Step 1: Get the Prompt

Accept inline text, file path, or ask the user.

### Step 2: Plan + Generate + Execute + Evaluate

Apply the **prompt-evaluation** skill's **Steps 1-4**:

1. **Plan** — Extract evaluation criteria from the prompt
2. **Generate Personas** — Create 3 diverse test personas
3. **Execute (Parallel)** — Launch **persona-executor** agents in parallel to run the prompt with each persona's request simultaneously
4. **Evaluate** — Score each criterion 1-5 with evidence

Present the final results as a score table with overall average.

### Step 3: Offer Next Steps

- "Score too low? Use `/improve-prompt` to get an improved version"
- "Want the **full pipeline** with improvement suggestions? Use `/evaluate-prompt`"
- "Want to **test with more personas**? Use `/generate-personas --count 5` then `/score-prompt`"
