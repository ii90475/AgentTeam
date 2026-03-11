# Definition Plan — Step by Step

## Approach

For each agent, we will:
1. Review the AoR (Area of Responsibility) together
2. Define inputs — what does this agent receive?
3. Define outputs — what does this agent produce?
4. Define constraints — what must it never do?
5. Define interactions — who does it talk to and when?
6. Define FailPoint tracking — how does it learn from mistakes?
7. Write the definition file
8. You review and approve

We work through one agent at a time, in process order.

## Order of Work

### Phase 1: New Definitions (5 agents)
These don't exist at all. Clean slate.

| Step | Agent | Why first |
|------|-------|-----------|
| 1 | Technology Analyst | First in process. Informs everything downstream. |
| 2 | Product Manager | Absorbs Planner. Needs clear boundary with BA. |
| 3 | Project Manager | Absorbs Context Keeper + docs. Runs throughout. |
| 4 | Tester | New agent. Absorbs test-builder + test-runner. |
| 5 | DevOps | New agent. Absorbs CI/CD. |

### Phase 2: Rewrites (3 agents)
These exist but need rewriting to match new team structure.

| Step | Agent | What changes |
|------|-------|-------------|
| 6 | Business Analyst | Review against new Product Manager boundary. May need scope adjustment. |
| 7 | Developer | Rewrite of Implementer. Absorbs scaffolding. New name, potentially new AoR. |
| 8 | Security | Review interactions — no longer reports to Validator. Standalone in chain. |

### Phase 3: Define from Scratch (1 agent)
| Step | Agent | Notes |
|------|-------|-------|
| 9 | QA Agent | Browser-based E2E. Last before DevOps in chain. |

### Phase 4: Cleanup
- Delete retired definition files
- Update README.md
- Update CLAUDE.md to reflect new team
- Update slash commands
- Update .claude/agents/ subagent definitions

## Current Step

**Step 1: Technology Analyst** — Ready when you are.
