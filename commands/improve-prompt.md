---
description: "Evaluate a prompt and suggest an improved version based on scoring feedback"
argument-hint: "<prompt text or file path>"
---

# /improve-prompt -- Evaluate and Improve a Prompt

Run the full evaluation pipeline and focus on delivering an improved version of the prompt with clear rationale for each change.

## Invocation

```
/improve-prompt "You are a helpful assistant. Answer questions."
/improve-prompt prompts/weak-prompt.txt
/improve-prompt                                     # asks for the prompt
```

## Workflow

### Step 1: Get the Prompt

Accept inline text, file path, or ask the user.

### Step 2: Run Full Pipeline with Improvement Focus

Apply the **prompt-evaluation** skill's **Steps 1-6**:

1. **Plan** — Extract evaluation criteria
2. **Generate Personas** — Create 3 test personas
3. **Execute** — Run prompt with each persona
4. **Evaluate** — Score each criterion
5. **Analyze** — Determine if improvable
6. **Rewrite** — Generate improved prompt

If the prompt is already `sufficient`, report the scores and confirm no changes needed.

**Output focus**: Present a clear before/after comparison:
- Original prompt
- Evaluation scores (brief summary)
- Improved prompt (full text)
- Table of changes with reasons

### Step 3: Offer Next Steps

- "Want to **evaluate the improved version**? Run `/evaluate-prompt` with the new prompt"
- "Want to **compare scores** before and after? Run `/score-prompt` on both versions"
- "Want to **iterate further**? Run `/improve-prompt` again on the improved version"
