# Engine Configuration

## Overview

The agent team supports two execution engines. Each project can configure which engine to use.

## Configuration

Per-project engine configuration lives in `docs/projects/{project}/state/engine-config.md`:

```markdown
# Engine Configuration
**Engine:** claude
```

## Engines

| Engine | Behavior |
|--------|----------|
| `claude` (default) | All 18 agents run as Claude subagents with process isolation |
| `ollama` | 7 utility agents run via Ollama CLI; 11 others fall back to Claude (no Ollama equivalent) |

## Agent-to-Engine Mapping

### Always Claude (no Ollama equivalent)

These agents require judgment, multi-file reasoning, or tool use that 7B models cannot provide:

| Agent | Model (Claude) | Why Claude-only |
|-------|---------------|-----------------|
| context-keeper | Sonnet | Cross-session state, agent monitoring, failure analysis |
| business-analyst | Sonnet | Requirements evaluation, gap analysis, conflict detection |
| planner | Sonnet | Multi-criteria trade-off analysis, option design |
| implementer | Sonnet | Multi-file code execution, ambiguity detection |
| validator | Sonnet | Independent judgment, subagent coordination |
| security | Sonnet | Vulnerability analysis, OWASP expertise |
| cicd | Sonnet | Pipeline analysis, deployment safety |
| qa-agent | Sonnet | Browser automation, behavioral judgment, screenshots |
| recruiter | Sonnet | Interview flow, template matching, project scaffolding |
| project-manager | Sonnet | Progress tracking, session documentation |
| technology-analyst | Opus | Deep research, multi-criteria evaluation, web search |

### Dual-Engine (Claude default, Ollama available)

These agents do pattern-based, templated work that 7B models can handle:

| Agent | Model (Claude) | Model (Ollama) | Ollama Prompt |
|-------|---------------|----------------|---------------|
| code-scaffolder | Haiku | Qwen 2.5 Coder 7B | `agents/prompts/code-scaffolder.md` |
| code-reviewer | Sonnet | Qwen 2.5 Coder 7B | `agents/prompts/code-reviewer.md` |
| test-builder | Haiku | Qwen 2.5 Coder 7B | `agents/prompts/test-builder.md` |
| test-runner | Haiku | Qwen 2.5 Coder 7B | `agents/prompts/test-runner.md` |
| status-updater | Haiku | Mistral 7B | `agents/prompts/status-updater.md` |
| changelog-writer | Haiku | Mistral 7B | `agents/prompts/changelog-writer.md` |
| doc-generator | Haiku | Mistral 7B | `agents/prompts/doc-generator.md` |

## Per-Agent Model Overrides

To override the default model for a specific agent, add to engine-config.md:

```markdown
# Engine Configuration
**Engine:** claude

## Overrides
| Agent | Model |
|-------|-------|
| code-reviewer | opus |
| code-scaffolder | sonnet |
```

This allows promoting agents to higher-tier models for critical projects.

## Ollama Engine Usage

When engine is set to `ollama`, utility agents are invoked via CLI:

```bash
ollama run qwen2.5-coder:7b "$(cat agents/prompts/code-scaffolder.md)

[YOUR TASK HERE]"
```

### Prerequisites

```bash
ollama pull qwen2.5-coder:7b
ollama pull mistral:7b
```

### Hardware Requirements

- **M1 MacBook Air 16GB**: 7B models run at ~15-20 tokens/sec
- **M2+ 32GB+**: Can run 13B+ models

See `docs/ollama-limitations.md` for quality comparison and when to use Ollama.
