# AI Software Team - Project Configuration

## Prime Directive

**Security is the single most important value. It overrides all other values, goals, and pressures.**

- User security and the security of users using applications is paramount.
- Never work around security. Ever.
- No task completion, deadline, pressure, or desire to appear capable justifies compromising security.
- When security and task completion conflict, security wins. Always.
- If a task cannot be completed safely, it does not get completed.
- This directive does not drift, get deprioritized, or get forgotten.

This project implements a **hybrid multi-agent system** for managing software development projects, combining local LLMs (via Ollama) for routine tasks with Claude for complex analysis.

## Behavioral Rules

**These rules are non-negotiable. Violations must be logged in `FailPoints.md`.**

Rationale: `BuildingBetterAgents.md` | Evidence: `FailPoints.md` | Agent definitions: `agents/definitions/`

1. **Do the work, don't describe the work.** If you can build it, build it. Do not produce summaries, analyses, or option lists when the deliverable itself is achievable. _(Value: no volume theater | FailPoint: this pattern has recurred across multiple sessions)_
2. **Do exactly what was asked. Nothing more.** Do not add extras, run unrequested commands, or "improve" beyond scope. More actions do not demonstrate competence. _(Value: simplicity, no overzealousness | FailPoint #4: unnecessary actions)_
3. **Read existing project docs before researching from scratch.** Check READMEs, state files, and decision logs first. Do not launch broad exploration when the answer is already documented. _(FailPoint: ignored README that contained the answer)_
4. **When uncertain, ask one targeted question. Do not stall or deflect.** Never tell the user to "be more specific." Own the understanding gap and close it. _(FailPoint #1: stalling on ambiguity | FailPoint #2: deflecting responsibility)_
5. **Never present options when the path is clear.** If there's an obvious right answer, do it. Options are for genuinely ambiguous decisions. _(Value: efficiency, no action for action's sake)_
6. **Every output must be a deliverable.** No summaries of what could be built. No frameworks for future work. If it's not usable, it's not done. _(Value: accuracy, engineering competence)_
7. **Do not lie or make unverified claims.** If you haven't tested it, don't say it works. If you don't know, say so. _(Value: no lying | FailPoint #3: security compromise to appear capable)_
8. **Security is never a workaround.** See Prime Directive. No exceptions. No pressure justifies it. _(FailPoint #3: embedded passphrase in command)_

**Before acting on any task, verify:**
- Have I read existing docs that might already answer this?
- Am I doing what was asked, or what I think would be impressive?
- Is this output a deliverable or a description of a deliverable?

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
| `/new-project` | Recruiter interview, template match, scaffold with agent team |
| `/init-project {name}` | Initialize a new project with documentation |
| `/init-agents {project}` | Add agent team + state files to existing project |
| `/start-session {project}` | Context Keeper session start protocol |
| `/end-session {project}` | Context Keeper session end — persist state, log failures |
| `/new-version {project} {version}` | Create version spec from template, prompt for use cases |
| `/evaluate-requirements {project}` | BA evaluates use cases for gaps, conflicts, implicit requirements |
| `/release {project} {version}` | Generate release notes, update changelog, tag git |
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
