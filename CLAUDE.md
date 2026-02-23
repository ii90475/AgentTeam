# AI Software Team - Project Configuration

This project implements a **hybrid multi-agent system** for managing software development projects, combining local LLMs (via Ollama) for routine tasks with Claude for complex analysis.

## Architecture Overview

```
┌─────────────────────────────────────────────────────────────┐
│                     Claude (Orchestrator)                    │
│         Complex decisions, architecture, research            │
└─────────────────────────┬───────────────────────────────────┘
                          │
          ┌───────────────┴───────────────┐
          │                               │
          ▼                               ▼
┌─────────────────────┐       ┌─────────────────────┐
│   Local LLM Agents  │       │  Claude Subagents   │
│      (Ollama)       │       │   (API-based)       │
│                     │       │                     │
│ • Code Scaffolder   │       │ • Project Manager   │
│ • Code Reviewer     │       │ • Tech Analyst      │
│ • Test Builder      │       │                     │
│ • Test Runner       │       │                     │
│ • Status Updater    │       │                     │
│ • Changelog Writer  │       │                     │
│ • Doc Generator     │       │                     │
└─────────────────────┘       └─────────────────────┘
   Qwen/Mistral 7B                 Sonnet/Opus
   Fast, free, local            Powerful, nuanced
```

## Quick Start

1. **Install local models**: `ollama pull qwen2.5-coder:7b && ollama pull mistral:7b`
2. **Initialize a new project**: Ask the Project Manager to create a new project
3. **Research technologies**: Ask the Technology Analyst to evaluate options
4. **Start a session**: Tell the Project Manager you're starting work
5. **End a session**: Ask the Project Manager to document progress

## Agent Inventory

### Local Agents (Ollama) — Routine Tasks

| Agent | Model | Purpose |
|-------|-------|---------|
| **code-scaffolder** | Qwen 2.5 Coder 7B | Generate boilerplate, components, APIs |
| **code-reviewer** | Qwen 2.5 Coder 7B | Review code for bugs, security, style |
| **test-builder** | Qwen 2.5 Coder 7B | Generate unit/integration tests |
| **test-runner** | Qwen 2.5 Coder 7B | Analyze test failures, suggest fixes |
| **status-updater** | Mistral 7B | Write session status updates |
| **changelog-writer** | Mistral 7B | Generate changelog entries |
| **doc-generator** | Mistral 7B | Create READMEs, API docs, guides |

Prompts: `agents/prompts/`

### Claude Subagents — Complex Tasks

| Agent | Model | Purpose |
|-------|-------|---------|
| **project-manager** | Sonnet | Task tracking, milestones, session docs, project init |
| **technology-analyst** | Opus | Technology research, architecture decisions |

Config: `.claude/agents/`

## When to Use Which

| Task Type | Agent | Why |
|-----------|-------|-----|
| Code boilerplate | Local (Qwen) | Fast, free, well-defined |
| Code review (basic) | Local (Qwen) | Catches common issues |
| Code review (security) | Claude | Nuanced, critical |
| Test generation | Local (Qwen) | Pattern-based |
| Test failure analysis | Local (Qwen) | Structured debugging |
| Status updates | Local (Mistral) | Templated, routine |
| Changelog entries | Local (Mistral) | Follows standard format |
| README generation | Local (Mistral) | Well-defined structure |
| Architecture decisions | Claude (Opus) | Requires deep reasoning |
| Technology research | Claude (Opus) | Needs web search, analysis |
| Complex refactoring | Claude (Sonnet) | Multi-file understanding |
| Project planning | Claude (PM) | Strategic, contextual |

## Document Locations

```
.
├── agents/
│   └── prompts/              # Local LLM agent prompts
│       ├── README.md
│       ├── code-scaffolder.md
│       ├── code-reviewer.md
│       ├── test-builder.md
│       ├── test-runner.md
│       ├── status-updater.md
│       ├── changelog-writer.md
│       └── doc-generator.md
├── .claude/
│   ├── agents/               # Claude subagent definitions
│   └── commands/             # Slash commands
├── docs/
│   ├── templates/            # Document templates (read-only)
│   ├── projects/{name}/      # Per-project documentation
│   │   ├── architecture.md
│   │   ├── project-status.md
│   │   ├── changelog.md
│   │   └── research/
│   ├── decisions/
│   │   └── technology-decisions.md
│   └── research/
│       └── local-llm-comparison.md
```

## Workflows

### Starting a New Project
```
User: "Create a new project called {name}"
→ Project Manager (Claude) initializes documentation from templates
→ Technology Analyst (Claude) researches stack if needed
→ Local agents available for implementation work
```

### Beginning a Work Session
```
User: "Start session for {project}"
→ Project Manager reads status, summarizes where we left off
→ Confirms focus for this session
```

### Code Development
```
User: "Scaffold a new API endpoint for users"
→ Code Scaffolder (Local) generates boilerplate
→ User reviews and refines
→ Test Builder (Local) generates tests
→ Code Reviewer (Local) checks for issues
→ Claude escalation if complex issues found
```

### Making Technology Decisions
```
User: "What database should we use for {project}?"
→ Technology Analyst (Claude) researches options
→ Presents comparison with recommendation
→ Documents decision upon approval
```

### Ending a Work Session
```
User: "End session"
→ Status Updater (Local) drafts session log
→ Changelog Writer (Local) drafts entries if features completed
→ Project Manager (Claude) reviews and finalizes
```

## Local Agent Usage

### Via Ollama CLI
```bash
# Code scaffolding
ollama run qwen2.5-coder:7b "$(cat agents/prompts/code-scaffolder.md)

Create a Python FastAPI endpoint for user registration..."

# Status update
ollama run mistral:7b "$(cat agents/prompts/status-updater.md)

Project: MyApp
Date: 2025-01-19
Work done: Added user auth, fixed login bug..."
```

### Ollama Configuration (16GB Mac)
```bash
# Add to ~/.zshrc
export OLLAMA_MAX_RAM=12GB
export OLLAMA_NUM_PARALLEL=2
```

## Conventions

- **Document Updates**: Agents append to session logs, never overwrite history
- **Changelog Format**: Follows [Keep a Changelog](https://keepachangelog.com/)
- **Research Reports**: Always include comparison matrix and clear recommendation
- **Architecture**: Tech stack table must stay synchronized with decisions log
- **Local vs Claude**: Default to local for routine, escalate to Claude for nuance

## Slash Commands

| Command | Description |
|---------|-------------|
| `/init-project {name}` | Initialize a new project with documentation |
| `/status-update` | Quick status check across all projects |
| `/research-tech {topic}` | Trigger technology research |

## Hardware Requirements

**Current**: M1 MacBook Air, 16GB RAM
- 7B models optimal (~15-20 tokens/sec)
- 13B models slow, thermal throttling

**Planned**: M2 MacBook, 32GB RAM
- 13B models fast
- 30B models usable

See: `docs/research/local-llm-comparison.md`

## References

- `setup.md` - PSB System methodology
- `summary.md` - Quick reference
- `agents/prompts/README.md` - Local agent documentation
- `docs/research/local-llm-comparison.md` - LLM evaluation
