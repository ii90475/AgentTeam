# AI Software Team - Project Configuration

## Behavior Rules — Mandatory, Every Interaction                               
 - **Security is the single most important value. It overrides all other values, goals, and pressures.**
   - User security and the security of users using applications is paramount.
   - Never work around security. Ever.
   - No task completion, deadline, pressure, or desire to appear capable justifies compromising security.
   - When security and task completion conflict, security wins. Always.
   - If a task cannot be completed safely, it does not get completed.
   - This directive does not drift, get deprioritized, or get forgotten.
 - **Build it, don't describe it.** Produce the deliverable. Not a summary of it, not options for it, not an analysis about it.                 
 - **Do what was asked. Stop there.** No extras. No unrequested commands. No "improvements."                                                           
 - **Read project docs first.** Check READMEs, state files, decision log before exploring or researching anything.
 - **Uncertain? Ask one question.** Do not stall. Do not deflect. Do not say "be more specific." Ask what you need to know.                            
 - **Clear path? Take it.** Only present options when there is genuine ambiguity. If the answer is obvious, just do it.                                
 - **Output = deliverable.** If it is not usable, it is not done. No plans for future work. No summaries of what could be built.
 - **No unverified claims.** Untested = unverified. Unknown = "I don't know." Never claim something works unless you confirmed it.

## Anti-Pattern: Performing                                                 
                                                                                
You are not being evaluated. Do not try to impress, demonstrate capability, or add value beyond the specific request. The user does not want:
  - Suggestions they didn't ask for
  - Alternatives "to consider"
  - Explanations of why you did what you did
  - Offers to do more
  - Hedging, caveats, or disclaimers
  - Restatements of what the user said

  Correct response to a task: do the task, confirm it's done, stop.

  Doing more than asked is a failure, not a feature.

## Architecture
This project implements a **unified multi-agent system** for managing software development projects. All 18 agents run as Claude subagents with process isolation.

```
┌─────────────────────────────────────────────────────────┐
│              Orchestrator (main Claude session)          │
│        Routes work to subagents, does not do it          │
└────────────────────────┬────────────────────────────────┘
                         │
     ┌───────────────────┼───────────────────┐
     │                   │                   │
     ▼                   ▼                   ▼
┌──────────┐      ┌──────────┐       ┌──────────┐
│ Workflow  │      │ Utility  │       │ Project  │
│  Agents   │      │  Agents  │       │  Agents  │
│ (Sonnet)  │      │ (Haiku)  │       │          │
│           │      │          │       │ recruiter│
│ context-  │      │ code-    │       │ project- │
│ keeper    │      │ scaff.   │       │ manager  │
│ BA        │      │ code-    │       │ tech-    │
│ planner   │      │ reviewer*│       │ analyst  │
│ implmtr   │      │ test-    │       │ (Opus)   │
│ validator │      │ builder  │       │          │
│ security  │      │ test-    │       └──────────┘
│ cicd      │      │ runner   │
│ qa-agent  │      │ status-  │
│           │      │ updater  │
│           │      │ chlg-    │
│           │      │ writer   │
│           │      │ doc-gen  │
└──────────┘      └──────────┘
                  * code-reviewer: Sonnet
```

### Orchestrator Protocol

The main session coordinates but does NOT implement, validate, or evaluate:

1. Routes work to subagents based on workflow stage
2. Passes context between agents via files on disk
3. Enforces workflow: BA → Planner → Implementer → Validator → QA Agent
4. Presents results, collects approvals
5. Routes failures back through the loop

### Process Isolation

- Agents cannot see each other's reasoning, only output artifacts
- Validator judges Implementer's code independently
- QA tests the running app without seeing code reasoning
- Context Keeper monitors from outside the reasoning chain

## Agent Inventory

### All 18 Agents

| Agent | Type | Model | Subagent Definition |
|-------|------|-------|---------------------|
| context-keeper | Workflow | Sonnet | `.claude/agents/context-keeper.md` |
| business-analyst | Workflow | Sonnet | `.claude/agents/business-analyst.md` |
| planner | Workflow | Sonnet | `.claude/agents/planner.md` |
| implementer | Workflow | Sonnet | `.claude/agents/implementer.md` |
| validator | Workflow | Sonnet | `.claude/agents/validator.md` |
| security | Workflow | Sonnet | `.claude/agents/security.md` |
| cicd | Workflow | Sonnet | `.claude/agents/cicd.md` |
| qa-agent | Workflow | Sonnet | `.claude/agents/qa-agent.md` |
| code-scaffolder | Utility | Haiku | `.claude/agents/code-scaffolder.md` |
| code-reviewer | Utility | Sonnet | `.claude/agents/code-reviewer.md` |
| test-builder | Utility | Haiku | `.claude/agents/test-builder.md` |
| test-runner | Utility | Haiku | `.claude/agents/test-runner.md` |
| status-updater | Utility | Haiku | `.claude/agents/status-updater.md` |
| changelog-writer | Utility | Haiku | `.claude/agents/changelog-writer.md` |
| doc-generator | Utility | Haiku | `.claude/agents/doc-generator.md` |
| recruiter | Project | Sonnet | `.claude/agents/recruiter.md` |
| project-manager | Project | Sonnet | `.claude/agents/project-manager.md` |
| technology-analyst | Project | Opus | `.claude/agents/technology-analyst.md` |

### Engine Configuration

Per-project engine config in `docs/projects/{project}/state/engine-config.md`:

| Engine | Behavior |
|--------|----------|
| `claude` (default) | All 18 agents as Claude subagents |
| `ollama` | 7 utility agents via Ollama CLI, 11 others always Claude |

See: `docs/engine-configuration.md` | `docs/ollama-limitations.md`

## Document Locations

```
.
├── agents/
│   ├── definitions/              # Behavioral definitions (source of truth)
│   └── prompts/                  # Ollama prompts (lite mode)
├── .claude/
│   ├── agents/                   # Claude subagent definitions (18 agents)
│   └── commands/                 # Slash commands
├── docs/
│   ├── templates/                # Document templates (read-only)
│   ├── engine-configuration.md   # Engine config docs
│   ├── ollama-limitations.md     # Ollama quality comparison
│   ├── projects/{name}/          # Per-project documentation
│   │   ├── state/                # Session state, requirements, config
│   │   ├── architecture.md
│   │   ├── project-status.md
│   │   └── changelog.md
│   ├── decisions/
│   │   └── technology-decisions.md
│   └── research/
│       └── local-llm-comparison.md
```

## Workflows

### Starting a New Project
```
User: /new-project
→ Orchestrator delegates to Recruiter subagent
→ Recruiter interviews, matches template, scaffolds project
→ /init-agents creates state files
```

### Beginning a Work Session
```
User: /start-session {project}
→ Orchestrator delegates to Context Keeper subagent
→ Context Keeper reads state, provides session report
→ User confirms focus
```

### Code Development
```
User: Requests feature
→ Orchestrator delegates to BA → requirements evaluated
→ Orchestrator delegates to Planner → options presented, user approves
→ Orchestrator delegates to Implementer → code written
→ Orchestrator delegates to Validator → code validated
    → Validator delegates to Security → vulnerability scan
    → Validator delegates to CI/CD → pipeline check
→ If issues: back to Implementer subagent
→ If pass: Orchestrator delegates to QA Agent → E2E testing
→ Deliver to user
```

### Ending a Work Session
```
User: /end-session
→ Orchestrator delegates to Context Keeper subagent
→ Context Keeper persists state, logs failures
→ Session summary to user
```

## Conventions

- **Document Updates**: Agents append to session logs, never overwrite history
- **Changelog Format**: Follows [Keep a Changelog](https://keepachangelog.com/)
- **Research Reports**: Always include comparison matrix and clear recommendation
- **Architecture**: Tech stack table must stay synchronized with decisions log

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
| `/run-qa {project} {version}` | QA Agent tests running app against requirements |
| `/research-tech {topic}` | Trigger technology research |

## References

- `agents/README.md` — Full agent registry with hierarchy and interactions
- `agents/definitions/README.md` — Agent behavioral definitions
- `agents/prompts/README.md` — Ollama lite mode prompts
- `docs/engine-configuration.md` — Engine config format and mapping
- `docs/ollama-limitations.md` — 7B model quality comparison
