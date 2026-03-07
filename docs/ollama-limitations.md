# Ollama Limitations

## Overview

The agent team defaults to Claude subagents for all 18 agents. Ollama is available as a lite mode for 7 utility agents, useful for offline work, cost reduction, or rapid prototyping.

This document covers what 7B models can and cannot do, quality differences, and when Ollama makes sense.

## Quality Comparison by Agent

| Agent | Claude Quality | Ollama Quality | Gap | Notes |
|-------|---------------|----------------|-----|-------|
| code-scaffolder | Excellent | Good | Small | Pattern-based work; Ollama handles well for common frameworks |
| code-reviewer | Excellent | Moderate | Medium | Ollama catches obvious issues but misses nuanced security/logic bugs |
| test-builder | Excellent | Good | Small | Standard test patterns work; edge case coverage weaker on Ollama |
| test-runner | Excellent | Good | Small | Failure analysis is structured; root cause depth limited on Ollama |
| status-updater | Excellent | Good | Small | Templated output; Ollama follows format reliably |
| changelog-writer | Excellent | Good | Small | Keep a Changelog format is well-structured; Ollama handles it |
| doc-generator | Excellent | Moderate | Medium | Complex docs (architecture, guides) noticeably weaker on Ollama |

## What 7B Models Can Do Well

- Generate boilerplate code for common frameworks (React, Express, FastAPI)
- Write standard unit tests with good coverage
- Follow structured output formats (changelogs, status updates)
- Analyze simple test failures with clear error messages
- Generate READMEs and basic documentation

## What 7B Models Cannot Do

- **Multi-file reasoning** — cannot understand cross-file dependencies
- **Nuanced security review** — misses subtle vulnerabilities
- **Complex architecture** — cannot reason about system design trade-offs
- **Requirements evaluation** — cannot detect implicit requirements or conflicts
- **Browser testing** — no tool use capability, no Playwright
- **Agent monitoring** — cannot observe and judge other agent behavior
- **Deep research** — no web search, limited knowledge
- **Long context** — degrades significantly beyond 4K tokens

## Agents Without Ollama Equivalents

These 11 agents have no Ollama option because their work requires capabilities beyond 7B models:

| Agent | Why No Ollama |
|-------|---------------|
| context-keeper | Requires cross-session reasoning, agent monitoring, failure pattern analysis |
| business-analyst | Requires nuanced requirements evaluation, gap detection, conflict analysis |
| planner | Requires multi-criteria trade-off analysis, architecture understanding |
| implementer | Requires multi-file code execution, ambiguity detection, verification |
| validator | Requires independent judgment, claim verification, subagent coordination |
| security | Requires deep vulnerability analysis, OWASP expertise, dependency auditing |
| cicd | Requires pipeline analysis, deployment safety evaluation |
| qa-agent | Requires Playwright browser automation, behavioral judgment, screenshot capture |
| recruiter | Requires conversational interview, template matching, project scaffolding |
| project-manager | Requires progress analysis, risk identification, strategic planning |
| technology-analyst | Requires web research, multi-criteria evaluation, deep reasoning |

## When to Use Ollama

**Good use cases:**
- Offline development (no internet required)
- Cost-sensitive prototyping (free, unlimited)
- Privacy-sensitive work (all processing local)
- Quick scaffolding of standard components
- Generating boilerplate tests for well-defined functions

**Avoid Ollama for:**
- Security-critical code review
- Complex architecture decisions
- Requirements with nuance or ambiguity
- Multi-file refactoring
- Production-ready documentation
- Anything requiring judgment beyond pattern matching

## Gap-Closing Strategies

If you must use Ollama for cost or offline reasons:

1. **Review Ollama output manually** — treat it as a draft, not a deliverable
2. **Use Claude for validation** — even if Ollama writes code, have Claude review it
3. **Keep context short** — 7B models work best with <2K token prompts
4. **One task per prompt** — don't combine multiple goals
5. **Provide examples** — 7B models perform much better with few-shot prompting
6. **Escalate complex work** — when Ollama output is poor, switch to Claude

## Configuration

See `docs/engine-configuration.md` for how to configure per-project engine settings.
