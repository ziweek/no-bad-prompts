---
description: "Extract evaluation criteria from a prompt — identify what to test without running the full pipeline"
argument-hint: "<prompt text or file path>"
---

# /plan-criteria -- Extract Evaluation Criteria

Analyze a prompt and extract specific, observable evaluation criteria without running the full evaluation pipeline.

## Invocation

```
/plan-criteria "You are a code reviewer. Focus on security vulnerabilities and performance issues."
/plan-criteria prompts/chatbot-prompt.txt
/plan-criteria                                     # asks for the prompt
```

## Workflow

### Step 1: Get the Prompt

Accept inline text, file path, or ask the user.

### Step 2: Generate Criteria

Apply the **prompt-evaluation** skill's **Step 1 (Plan)** only:

- Extract 3-7 evaluation criteria from the prompt
- Each criterion quotes the prompt directly
- Each tests a single, clear judgment

### Step 3: Offer Next Steps

- "Want to **test these criteria** with diverse personas? Use `/score-prompt`"
- "Want to **generate test personas** for this prompt? Use `/generate-personas`"
- "Want to **run the full evaluation**? Use `/evaluate-prompt`"
