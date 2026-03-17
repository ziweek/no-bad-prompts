---
description: "Run a full interactive prompt evaluation pipeline — generate criteria, create test personas, execute, score, and suggest improvements, with user feedback at each step"
argument-hint: "<prompt text or file path>"
---

# /evaluate-prompt -- Full Interactive Prompt Evaluation

Run the complete 6-step prompt evaluation pipeline interactively. Pause after each major step to gather user feedback before proceeding.

## Invocation

```
/evaluate-prompt "You are a customer service agent. Always greet by name. Keep responses under 3 sentences."
/evaluate-prompt prompts/my-system-prompt.txt
/evaluate-prompt                                   # asks for the prompt
```

## Workflow

### Step 1: Get the Prompt

Accept from:
- Inline text argument
- File path (read the file contents)
- If no argument, ask the user to provide the prompt

### Step 2: Run Interactive Pipeline

Apply the **prompt-evaluation** skill, executing all 6 steps in order. **Pause after each step** to ask the user for feedback before proceeding.

**Step 2a: Plan — Generate Criteria**
- Extract 3-7 evaluation criteria from the prompt
- Present criteria to the user
- Ask: "이 평가 기준으로 진행할까요? 추가하거나 수정하고 싶은 기준이 있으면 말씀해 주세요."
- If the user suggests changes, adjust criteria before continuing

**Step 2b: Generate Personas**
- Create 3 diverse test personas with realistic user requests
- Present personas to the user
- Ask: "이 페르소나들로 테스트를 진행할까요? 추가하거나 변경하고 싶은 페르소나가 있으면 말씀해 주세요."
- If the user suggests changes, adjust personas before continuing

**Step 2c: Execute (Parallel Agents)**
- Launch **persona-executor** agents in parallel — one per persona — using the Agent tool
- All agents must be launched in a single message for true parallel execution
- Collect all responses and present execution results
- Ask: "실행 결과를 확인하셨나요? 평가를 진행할까요?"
- Proceed to evaluation

**Step 2d: Evaluate**
- Score each criterion 1-5 with evidence from responses
- Present score table with overall average
- Ask: "평가 결과에 동의하시나요? 프롬프트 개선 분석을 진행할까요?"
- Proceed to analysis

**Step 2e: Analyze + Rewrite**
- Determine if the prompt is `improvable` or `sufficient`
- If improvable, suggest an improved version with change rationale
- Present final results

### Step 3: Offer Next Steps

- "Want to **evaluate the improved version**? Run `/evaluate-prompt` again with the new prompt"
- "Want to **generate more personas** for deeper testing? Use `/generate-personas`"
- "Want to **quickly re-score** without the interactive flow? Use `/score-prompt`"

## Notes

- The interactive flow gives users control over each step — they can adjust criteria, add personas, or skip steps
- For a faster non-interactive evaluation, users can use `/score-prompt` (no pauses) or `/improve-prompt` (focused on improvement output)
- When the user says "진행" / "네" / "yes" / "좋아" or similar, proceed to the next step without changes
