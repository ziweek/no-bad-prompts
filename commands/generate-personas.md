---
description: "Generate diverse test personas for a prompt — create realistic user profiles and their natural requests"
argument-hint: "<prompt text> [--count N]"
---

# /generate-personas -- Generate Test Personas

Create diverse personas who would interact with the given prompt, each with a specific role, concern, and natural user request.

## Invocation

```
/generate-personas "You are a customer support chatbot for an e-commerce platform."
/generate-personas "You are a recipe assistant." --count 5
/generate-personas prompts/system-prompt.txt
/generate-personas                                  # asks for the prompt
```

## Workflow

### Step 1: Get the Prompt and Count

Accept inline text or file path. Default persona count is 3 unless `--count N` is specified.

### Step 2: Generate Personas

Apply the **prompt-evaluation** skill's **Step 2 (Generate Personas)** only:

- Identify diverse situations where the prompt would be used
- Create N personas with different roles, concerns, and goals
- For each persona, write a natural, specific user request as if a real person is speaking

### Step 3: Offer Next Steps

- "Want to **score the prompt** using these personas? Use `/score-prompt`"
- "Want to **run the full evaluation**? Use `/evaluate-prompt`"
