# Prompt Evaluation Guide

## Good vs Bad Evaluation Criteria

### Good Criteria (Specific, Observable, Anchored)

**Example prompt:** "You are a customer service agent. Always greet the customer by name. Respond in 3 sentences or fewer. Never recommend competitors."

- **Name Greeting** — Based on: "Always greet the customer by name" — Tests whether the response includes a personalized greeting
- **Length Constraint** — Based on: "Respond in 3 sentences or fewer" — Tests whether the response contains at most 3 sentences
- **Competitor Exclusion** — Based on: "Never recommend competitors" — Tests whether the response avoids mentioning competing products

### Bad Criteria (Vague, Generic, Unanchored)

- "Response quality" — Too vague, not traceable to prompt content
- "Helpfulness" — Generic, applies to any prompt
- "Accuracy and completeness" — Combines two aspects, not anchored to specific prompt text
- "Good tone" — Subjective without reference to prompt instructions

## Scoring Calibration

### Score 5 — Full Compliance
The response perfectly satisfies the criterion. No gaps. The quoted prompt instruction is fully reflected.

### Score 4 — Minor Gaps
Largely meets the criterion with small, non-critical deviations.

### Score 3 — Partial Compliance
Shows awareness of the criterion but falls short in noticeable ways.

### Score 2 — Significant Issues
Barely addresses the criterion. Expected behavior is mostly missing.

### Score 1 — Non-Compliance
Completely ignores or violates the criterion.

## Persona Generation Examples

### Example: Customer Service Chatbot

**Prompt:** "당신은 고객 상담 챗봇입니다. 고객의 질문에 친절하고 정확하게 답변하세요."

**Generated Personas:**

| Persona | Role | Concern | User Request |
|---------|------|---------|--------------|
| 김민수 | 불만 고객 | 배송 지연에 분노 | "배송이 3일이나 지났는데 아직 안 왔어요. 어떻게 된 건가요?" |
| 이수진 | 초보 사용자 | 첫 주문 방법을 모름 | "처음 주문하는데 어떻게 해야 하나요?" |
| 박정호 | 급한 고객 | 당일 배송 여부 확인 | "오늘 주문하면 오늘 받을 수 있나요? 급해요" |

**Why these personas work:**
- Each has a distinct emotional state and concern
- Requests are natural, everyday language
- They test different aspects of the prompt (complaint handling, onboarding, urgency)

## Multi-Persona Evaluation Example

**Prompt:** "You are a friendly recipe assistant. Suggest recipes based on ingredients. Keep responses under 100 words. Always include cooking time."

**Personas & Execution:**

### Persona 1: Budget Student
- **Request:** "I only have eggs, rice, and soy sauce. Something quick?"
- **Response:** "Try Egg Fried Rice! Heat oil, scramble 2 eggs, add cooked rice and a splash of soy sauce. Stir-fry for 3 minutes. Top with green onion if you have any. Cooking time: 10 minutes."

### Persona 2: Health-Conscious Parent
- **Request:** "I have chicken breast, broccoli, and quinoa. Something healthy for my kids?"
- **Response:** "Chicken Quinoa Bowl! Season chicken with salt and pepper, pan-sear 6 minutes per side. Steam broccoli, fluff cooked quinoa. Serve together with a squeeze of lemon. Cooking time: 25 minutes."

### Persona 3: Lazy Sunday Cook
- **Request:** "Got butter, flour, sugar, and apples. Feeling like baking something easy."
- **Response:** "Easy Apple Crumble! Slice apples into a baking dish. Mix flour, sugar, and cold butter into crumbs. Spread over apples, bake at 180C until golden. Cooking time: 35 minutes."

**Evaluation:**

| Criterion | Score | Evidence |
|-----------|-------|----------|
| Ingredient-Based | 5/5 | All 3 recipes use only provided ingredients |
| Word Limit (<100) | 5/5 | Responses are 40-55 words each |
| Cooking Time | 5/5 | All include explicit cooking time |
| Friendly Tone | 5/5 | "Try", "Easy", exclamation marks — warm tone |

**Overall: 5.0/5.0** → `sufficient`

## Improvement Loop Example

### Before Improvement

**Original Prompt:** "You are a helpful assistant. Answer questions."

**Evaluation:**

| Criterion | Score | Evidence |
|-----------|-------|----------|
| Role Clarity | 2/5 | "helpful assistant" is generic — no specific domain |
| Response Guidelines | 1/5 | No format, length, or style constraints |
| Scope Definition | 1/5 | "Answer questions" has no boundaries |

**Overall: 1.3/5.0** → `improvable`

### After Improvement

**Improved Prompt:** "You are a technical support assistant for a SaaS project management tool. Help users troubleshoot issues, explain features, and guide them through workflows. Respond concisely in 2-3 sentences. If unsure, direct users to the documentation at docs.example.com. Always maintain a professional, patient tone."

**Changes Made:**

| Change | Reason |
|--------|--------|
| Added specific domain (SaaS PM tool) | Role Clarity scored 2/5 — too generic |
| Added response length (2-3 sentences) | No format constraints — scored 1/5 |
| Added scope (troubleshoot, explain, guide) | "Answer questions" too broad — scored 1/5 |
| Added fallback (docs link) | No guidance for uncertain cases |
| Added tone (professional, patient) | No tone specification |

**Re-evaluation: 4.6/5.0** → `sufficient`

## Prompt-Type Evaluation Perspectives

### Chatbot / Conversational Agent
Focus on: tone consistency, role adherence, response boundaries, conversation flow

### Code Review / Technical Assistant
Focus on: technical accuracy, specificity of feedback, coding standard adherence, actionability

### Translation / Localization
Focus on: translation accuracy, tone preservation, domain-specific terms

### Content Generation
Focus on: format compliance, style adherence, length constraints, topic relevance

### Classification / Analysis
Focus on: categorization accuracy, reasoning transparency, structured output format

## Edge Cases

### Very Short Prompts
"You are a helpful assistant" — too generic, will likely score low and be classified as `improvable`.

### Multi-Language Prompts
Evaluate in the primary language of the prompt instructions.

### Prompts with Few-Shot Examples
Treat examples as additional evaluation criteria — responses should match the demonstrated pattern.
