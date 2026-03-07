# Agent Definitions

This directory contains the behavioral definitions for the AI agent team. These definitions are the **source of truth** for agent behavior — both Claude subagents and Ollama prompts reference these files.

## Agents

| Agent | Role |
|-------|------|
| [Context Keeper](context-keeper.md) | Memory, state, context tracking, failure management |
| [Business Analyst](business-analyst.md) | Requirements, scope, success criteria |
| [Planner](planner.md) | Options, recommendations, approval |
| [Implementer](implementer.md) | Minimal execution, stops on ambiguity |
| [Validator](validator.md) | Validates output against requirements and values |
| [Security](security.md) | Vulnerability and security checks (subagent) |
| [CI/CD](cicd.md) | Pipeline and deployment checks (subagent) |
| [QA Agent](qa-agent.md) | Browser-based E2E testing, behavioral verification |

## How Agents Are Invoked

All agents run as **Claude subagents** with process isolation. The orchestrator (main Claude session) delegates work to the appropriate subagent, which reads its behavioral definition from this directory.

Subagent definitions: `.claude/agents/` — each contains YAML frontmatter (name, description, tools, model) and references the behavioral definition here.

### Invocation via Slash Commands

| Skill | Purpose | Status |
|-------|---------|--------|
| `/start-session {project}` | Delegates to Context Keeper subagent | Implemented |
| `/end-session {project}` | Delegates to Context Keeper subagent | Implemented |
| `/init-agents {project}` | Initialize agent team + state files for existing project | Implemented |
| `/new-project` | Delegates to Recruiter subagent | Implemented |
| `/new-version {project} {version}` | Create version spec from template, prompt for use cases | Implemented |
| `/evaluate-requirements {project}` | Delegates to Business Analyst subagent | Implemented |
| `/release {project} {version}` | Generate release notes, update changelog, tag git | Implemented |
| `/run-qa {project} {version}` | Delegates to QA Agent subagent | Implemented |

---

## Setup

### For New Projects

Run `/new-project` — scaffolds CLAUDE.md with agent team reference and creates state files automatically.

### For Existing Projects

Run `/init-agents {project}` — adds agent team to existing project and creates state files.

### Workflow

```
Session Start
    → Orchestrator delegates to Context Keeper subagent
    → Context Keeper reads state, provides report
    → User confirms focus

New Version
    → /new-version creates version spec
    → User writes use cases
    → Orchestrator delegates to BA subagent for evaluation
    → User approves requirements

Work Request
    → Orchestrator delegates to Planner subagent
    → Planner presents options, waits for approval
    → Orchestrator delegates to Implementer subagent
    → Implementer executes approved plan
    → Orchestrator delegates to Validator subagent
    → Validator checks output
        ├── Delegates to Security subagent
        └── Delegates to CI/CD subagent
    → If issues: back to Implementer subagent
    → If pass: Orchestrator delegates to QA Agent subagent
        ├── If fail: back to Implementer subagent
        └── If pass: deliver to user

Release
    → /release generates release notes, updates changelog, tags git

Session End
    → Orchestrator delegates to Context Keeper subagent
    → Context Keeper logs state
    → FailPoints.md updated if failures occurred
```

## State Files

Context Keeper maintains these files (per project):

```
state/
├── session-log.md      # Running log of sessions
├── decisions.md        # Key decisions made
├── requirements.md     # Current requirements (synced with BA)
├── last-review.md      # Date of last periodic review
├── qa-config.md        # QA Agent configuration (URL, approval mode)
└── engine-config.md    # Engine configuration (claude/ollama)
```

## Templates

| Template | Purpose | Location |
|----------|---------|----------|
| Application Spec | Per-app: overview, architecture, security, deployment | `docs/templates/application-spec-template.md` |
| Version Spec | Per-release: use cases, requirements, tests, release notes | `docs/templates/version-spec-template.md` |

## Related Documentation

- [Agent Registry](../README.md) — Full agent inventory, hierarchy, interactions
- [Evaluation Criteria](../evaluation/criteria.md) — How agents are measured
- [Agent Updates](../changelog/agent-updates.md) — Version history
- [Engine Configuration](../../docs/engine-configuration.md) — Claude vs Ollama setup
- [Ollama Limitations](../../docs/ollama-limitations.md) — 7B model capabilities and gaps
- [FailPoints](../../FailPoints.md) — Claude behavioral failures log
- [BuildingBetterAgents](../../BuildingBetterAgents.md) — Values and principles
