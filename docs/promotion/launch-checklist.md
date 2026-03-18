# Launch Checklist

## Pre-launch (before any posting)

- [ ] PR #1 merged (README improvements + examples)
- [ ] GitHub About description set: `Automated prompt quality evaluation for Claude Code — test, score, and improve your prompts with persona-based testing. Zero setup.`
- [ ] GitHub Topics set: `claude-code`, `claude`, `prompt-engineering`, `llm`, `evaluation`, `ai-tools`, `quality-assurance`, `prompt-testing`
- [ ] GitHub Website URL set: `https://github.com/ziweek/no-bad-prompts#quick-start`
- [ ] Social preview image (OG image) uploaded in GitHub repo settings
- [ ] Terminal demo GIF recorded and added to README (replace placeholder)
- [ ] Test the install commands work: `/plugin marketplace add ziweek/no-bad-prompts` then `/plugin install no-bad-prompts@ziweek-no-bad-prompts`

## Posting Schedule

| Day | Action | File |
|-----|--------|------|
| D-day | Show HN post + first comment | `show-hn.md` |
| D+1~2 | r/ClaudeAI post | `reddit-claude-ai.md` |
| D+3~4 | r/PromptEngineering post | `reddit-prompt-engineering.md` |
| D+7 | Submit to awesome-claude-code list (if exists) | — |
| D+7 | Submit to awesome-prompt-engineering list | — |

## Optimal Posting Times

- **Hacker News:** Tue–Thu, 8–10 AM US Eastern (10 PM–midnight KST)
- **Reddit:** Tue–Thu, 9–11 AM US Eastern (11 PM–1 AM KST)

## Comment Response Guide

### Common questions and suggested responses

**"Why not just test manually?"**
> Manual testing is fine for simple prompts, but it's biased toward scenarios you already thought of. Persona-based testing surfaces edge cases you'd miss — like a user who asks about a competitor when your prompt says "never recommend competitors."

**"Does this work with other LLMs / not just Claude?"**
> Currently it's a Claude Code plugin, so it runs within Claude Code. The evaluation methodology (criteria extraction + persona testing) could be applied to any LLM though.

**"How is this different from existing eval frameworks?"**
> Most eval frameworks use pre-defined rubrics or benchmarks. This tool derives criteria from your specific prompt text — so the evaluation is always tailored to what your prompt actually promises to do.

**"Can I use this for production prompt monitoring?"**
> It's designed for development-time evaluation right now — testing before deployment. Production monitoring is a different problem that would need integration with your serving infrastructure.

## Post-launch Follow-up

- [ ] Track GitHub stars daily for the first week
- [ ] Check GitHub Insights > Traffic for README views
- [ ] Collect interesting feedback or feature requests from comments
- [ ] If a post gains traction, share it on X/Twitter with a brief thread
- [ ] Plan v0.3 update based on community feedback
