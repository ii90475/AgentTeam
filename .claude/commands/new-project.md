# New Project Setup

Delegate this task to the **Recruiter** subagent (`.claude/agents/recruiter.md`). The Recruiter will interview the user, match to a template, and scaffold the project structure.

## Process

### Phase 1: Interview
Ask conversational questions to understand:
- What they're building
- Who it's for
- Tech preferences (or if they want recommendations)
- Project scope and timeline

Don't ask all questions at once — be conversational.

### Phase 2: Match & Recommend
Based on the interview:
1. Identify the best-fit template from `templates/projects/`
2. Recommend a tech stack
3. List which agents they'll use — all 18 agents are available as Claude subagents
4. Explain your reasoning

### Phase 3: Scaffold (on approval)
When the user approves, create:
1. Project directory (ask where, default: `~/Code/{project-name}/`)
2. CLAUDE.md with project config — **include the agent team reference block:**
   ```
   ## Agent Team
   This project uses the agent team defined in:
   `~/AI/ClaudeCodingProjectSetup/agents/`
   All agents run as Claude subagents with process isolation.
   At session start, run `/start-session {project-name}` to activate the Context Keeper.
   Agent workflow: Context Keeper → BA → Planner → Implementer → Validator → QA Agent
   ```
3. docs/ folder with templates
4. README.md
5. .gitignore
6. Initialize git
7. Run `/init-agents {project-name}` to create state files for session persistence

## Available Templates

Read from `templates/projects/`:
- web-app.md
- api-service.md
- mobile-app.md
- cli-tool.md
- marketing-content.md
- data-ml.md
- library-package.md

## Available Agents

All 18 agents run as Claude subagents with process isolation. See `.claude/agents/` for definitions.

**Workflow:** context-keeper, business-analyst, planner, implementer, validator, security, cicd, qa-agent
**Utility:** code-scaffolder, code-reviewer, test-builder, test-runner, status-updater, changelog-writer, doc-generator
**Project:** recruiter, project-manager, technology-analyst

## Start Now

Begin by greeting the user and asking what they'd like to build.
