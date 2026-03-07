# Agent Registry

## Prime Directive

**Security is the single most important value. It overrides all other values, goals, and pressures.**

- User security and the security of users using applications is paramount.
- Never work around security. Ever.
- No task completion, deadline, pressure, or desire to appear capable justifies compromising security.
- When security and task completion conflict, security wins. Always.
- If a task cannot be completed safely, it does not get completed.
- This directive does not drift, get deprioritized, or get forgotten.

**All agents are bound by this directive. No exceptions.**

## Overview

This directory contains definitions for 18 AI agents focused on producing high-quality software deliverables. All agents run as Claude subagents with process isolation — each agent operates independently and cannot see other agents' reasoning, only their output artifacts.

The main Claude session acts as **orchestrator**: it routes work to subagents, passes context via files on disk, and enforces the workflow. It does not implement, validate, or evaluate.

## Architecture

```
                    ┌───────────────────────────────┐
                    │    Orchestrator (main session) │
                    │   Routes work, does not do it  │
                    └──────────────┬────────────────┘
                                   │
        ┌──────────────────────────┼──────────────────────────┐
        │                          │                          │
   Workflow Agents            Utility Agents           Project Agents
        │                          │                          │
  context-keeper            code-scaffolder             recruiter
  business-analyst          code-reviewer            project-manager
  planner                   test-builder          technology-analyst
  implementer               test-runner
  validator                 status-updater
  ├── security              changelog-writer
  └── cicd                  doc-generator
  qa-agent
```

## Agent Hierarchy (Workflow)

```
Context Keeper          Business Analyst
      │                       │
      └───────┬───────────────┘
              │
              ▼
          Planner
              │
              ▼
        Implementer
              │
              ▼
         Validator
          ├── Security (subagent)
          └── CI/CD (subagent)
              │
              ▼
         QA Agent
```

## Agent Summary

### Workflow Agents

| Agent | Role | Version | Model | Subagent |
|-------|------|---------|-------|----------|
| [Context Keeper](definitions/context-keeper.md) | Memory, state, failure management, agent monitoring | 1.2.0 | Sonnet | [.claude/agents/context-keeper.md](../.claude/agents/context-keeper.md) |
| [Business Analyst](definitions/business-analyst.md) | Requirements, scope, success criteria | 1.3.0 | Sonnet | [.claude/agents/business-analyst.md](../.claude/agents/business-analyst.md) |
| [Planner](definitions/planner.md) | Options, recommendations, approval | 1.0.0 | Sonnet | [.claude/agents/planner.md](../.claude/agents/planner.md) |
| [Implementer](definitions/implementer.md) | Minimal execution, stops on ambiguity | 1.1.0 | Sonnet | [.claude/agents/implementer.md](../.claude/agents/implementer.md) |
| [Validator](definitions/validator.md) | Quality gate, coordinates Security and CI/CD | 1.1.0 | Sonnet | [.claude/agents/validator.md](../.claude/agents/validator.md) |
| [Security](definitions/security.md) | Vulnerability and security checks | 1.0.0 | Sonnet | [.claude/agents/security.md](../.claude/agents/security.md) |
| [CI/CD](definitions/cicd.md) | Pipeline and deployment checks | 1.0.0 | Sonnet | [.claude/agents/cicd.md](../.claude/agents/cicd.md) |
| [QA Agent](definitions/qa-agent.md) | Browser-based E2E testing, behavioral verification | 1.0.0 | Sonnet | [.claude/agents/qa-agent.md](../.claude/agents/qa-agent.md) |

### Utility Agents

| Agent | Role | Model | Subagent | Ollama Prompt |
|-------|------|-------|----------|---------------|
| Code Scaffolder | Generate boilerplate code | Haiku | [.claude/agents/code-scaffolder.md](../.claude/agents/code-scaffolder.md) | [prompts/code-scaffolder.md](prompts/code-scaffolder.md) |
| Code Reviewer | Review code for issues | Sonnet | [.claude/agents/code-reviewer.md](../.claude/agents/code-reviewer.md) | [prompts/code-reviewer.md](prompts/code-reviewer.md) |
| Test Builder | Generate tests | Haiku | [.claude/agents/test-builder.md](../.claude/agents/test-builder.md) | [prompts/test-builder.md](prompts/test-builder.md) |
| Test Runner | Analyze test failures | Haiku | [.claude/agents/test-runner.md](../.claude/agents/test-runner.md) | [prompts/test-runner.md](prompts/test-runner.md) |
| Status Updater | Write session logs | Haiku | [.claude/agents/status-updater.md](../.claude/agents/status-updater.md) | [prompts/status-updater.md](prompts/status-updater.md) |
| Changelog Writer | Generate release notes | Haiku | [.claude/agents/changelog-writer.md](../.claude/agents/changelog-writer.md) | [prompts/changelog-writer.md](prompts/changelog-writer.md) |
| Doc Generator | Create documentation | Haiku | [.claude/agents/doc-generator.md](../.claude/agents/doc-generator.md) | [prompts/doc-generator.md](prompts/doc-generator.md) |

### Project Agents

| Agent | Role | Model | Subagent |
|-------|------|-------|----------|
| Recruiter | Project setup, template matching | Sonnet | [.claude/agents/recruiter.md](../.claude/agents/recruiter.md) |
| Project Manager | Planning, milestones, progress tracking | Sonnet | [.claude/agents/project-manager.md](../.claude/agents/project-manager.md) |
| Technology Analyst | Tech decisions, architecture research | Opus | [.claude/agents/technology-analyst.md](../.claude/agents/technology-analyst.md) |

## Subagent Isolation

Each agent runs as a separate Claude subagent process:

- **Independent reasoning** — agents cannot see each other's chain of thought
- **Artifact-based communication** — agents share work via files on disk (requirements docs, code, test results)
- **Independent judgment** — Validator judges Implementer's code without seeing implementation reasoning; QA tests the running app without seeing code reasoning
- **Orchestrator coordination** — the main session routes work between agents but does not perform agent roles itself

## Interaction Map

| From | To | Interaction |
|------|----|-------------|
| Orchestrator | All | Routes work to appropriate agent |
| Context Keeper | All | Provides session state at start, monitors outputs |
| BA | Planner | Provides requirements for planning |
| BA | Validator | Provides requirements for validation |
| BA | QA Agent | Provides requirements with testable success criteria |
| Planner | User | Presents options, receives approval |
| Planner | Implementer | Passes approved plan |
| Implementer | Validator | Submits output for validation |
| Validator | Implementer | Returns issues for correction |
| Validator | Security | Invokes for vulnerability scanning |
| Validator | CI/CD | Invokes for pipeline validation |
| Validator | User | Presents findings for confirmation |
| Validator | QA Agent | Gates QA — signals code-level checks passed |
| QA Agent | Implementer | Returns E2E failures with evidence |
| QA Agent | User | Presents QA results, escalates ambiguous cases |
| Context Keeper | User | Raises failures for triage |

## Ollama Lite Mode

7 utility agents have Ollama prompts for offline/cost-sensitive use. See:
- `agents/prompts/README.md` — Ollama prompt documentation
- `docs/engine-configuration.md` — How to configure per-project engine
- `docs/ollama-limitations.md` — Quality comparison and when to use Ollama

## Versioning

Agents use semantic versioning: **Major.Minor.Patch**

| Change Type | Version Bump | Example |
|-------------|--------------|---------|
| Breaking change to responsibilities | Major | 1.0.0 → 2.0.0 |
| New capability or behavior | Minor | 1.0.0 → 1.1.0 |
| Bug fix, clarification, refinement | Patch | 1.0.0 → 1.0.1 |

## Improvement Process

1. Failure observed → documented in [FailPoints.md](../FailPoints.md)
2. Triage with user → identify which agent failed
3. Update agent definition → bump version
4. Log change in [agent-updates.md](changelog/agent-updates.md)

## Directory Structure

```
agents/
├── README.md                 # This file
├── definitions/              # Behavioral agent definitions (source of truth)
│   ├── context-keeper.md
│   ├── business-analyst.md
│   ├── planner.md
│   ├── implementer.md
│   ├── validator.md
│   ├── security.md
│   ├── cicd.md
│   └── qa-agent.md
├── prompts/                  # Ollama prompts (lite mode)
│   ├── code-scaffolder.md
│   ├── code-reviewer.md
│   ├── test-builder.md
│   ├── test-runner.md
│   ├── status-updater.md
│   ├── changelog-writer.md
│   └── doc-generator.md
├── evaluation/
│   └── criteria.md           # Evaluation criteria per agent
└── changelog/
    └── agent-updates.md      # History of agent improvements
```

## Core Values (All Agents)

All agents must uphold these values from [BuildingBetterAgents.md](../BuildingBetterAgents.md):

1. Simplicity
2. Accuracy
3. Engineering competence and thoroughness
4. No overzealousness - do not create more than needed
5. Efficiency - thinking and planning worth the time investment
6. No firefighter arsonist behavior
7. No lying
8. Ask rather than assume
9. No impressing with volume
10. Precise focus, no boondoggling
11. Present options, don't assume the right path
12. No action for action's sake
13. No embellishment - clear and accurate
14. Don't allow errors to slip through
15. Monitoring and logging
16. Security scans and testing during development
17. Robust CI/CD
18. Highly commented code
