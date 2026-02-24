# Agent Definitions

This directory contains the definitions for the AI agent team focused on producing high-quality software deliverables.

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

## How to Invoke This Agent Team

### Option 1: CLAUDE.md Integration

Add to any project's CLAUDE.md:

```markdown
## Agent Team

This project uses the agent team defined in:
`~/AI/ClaudeCodingProjectSetup/agents/`

At session start, read and follow:
- `agents/README.md` - Agent hierarchy and interactions
- `agents/definitions/context-keeper.md` - Start with this agent

Follow the agent workflow:
1. Context Keeper provides session start report
2. BA owns requirements
3. Planner presents options, waits for approval
4. Implementer executes minimally
5. Validator checks all output
```

### Option 2: Skills/Commands

Skills in `.claude/commands/`:

| Skill | Purpose | Status |
|-------|---------|--------|
| `/start-session {project}` | Context Keeper session start/end protocol | Implemented |
| `/init-agents {project}` | Initialize agent team + state files for existing project | Implemented |
| `/new-project` | Recruiter interview + scaffolds with agent team reference | Updated |

### Option 3: Symlink Agent Definitions

For any project, symlink the agents folder:

```bash
ln -s ~/AI/ClaudeCodingProjectSetup/agents ~/Code/YourProject/agents
```

Then reference in project's CLAUDE.md.

---

## Setup

### For New Projects

Run `/new-project` — scaffolds CLAUDE.md with agent team reference and creates state files automatically.

### For Existing Projects

Run `/init-agents {project}` — adds agent team to existing project and creates state files.

### Session Start Protocol

At the start of each session, Context Keeper should:

1. Read previous session state
2. Read FailPoints.md for recent patterns
3. Check if periodic review is due (>7 days)
4. Provide performance report:
   - Agent health summary
   - Context health
   - Pending issues
5. Summarize: "Last session we [X]. Pending: [Y]. Open decisions: [Z]."
6. Confirm focus for this session

### Workflow

```
Session Start
    → Context Keeper reads state, provides report
    → User confirms focus

Work Request
    → BA gathers/confirms requirements
    → Planner presents options, waits for approval
    → Implementer executes approved plan
    → Validator checks output
        ├── Security subagent scans
        └── CI/CD subagent validates
    → If issues: back to Implementer
    → If pass: deliver to user

Session End
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
└── last-review.md      # Date of last periodic review
```

## Related Documentation

- [Agent Registry](../README.md) - Hierarchy, interactions, versioning
- [Evaluation Criteria](../evaluation/criteria.md) - How agents are measured
- [Agent Updates](../changelog/agent-updates.md) - Version history
- [FailPoints](../../FailPoints.md) - Claude behavioral failures log
- [BuildingBetterAgents](../../BuildingBetterAgents.md) - Values and principles
