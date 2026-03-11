# Software Development Team — Working Roster

## Status: DRAFT — Under Definition

| # | Role | Model | Definition File | Status |
|---|------|-------|-----------------|--------|
| 0 | Product Owner | Human | N/A | Active (James) |
| 1 | Technology Analyst | Opus | technology-analyst.md | NOT DEFINED |
| 2 | Product Manager | Sonnet | product-manager.md | NOT DEFINED |
| 3 | Business Analyst | Sonnet | business-analyst.md | NEEDS REWRITE |
| 4 | Project Manager | Sonnet | project-manager.md | NOT DEFINED |
| 5 | Developer | Sonnet | developer.md | NEEDS REWRITE |
| 6 | Tester | Haiku | tester.md | NOT DEFINED |
| 7 | Security | Sonnet | security.md | NEEDS REWRITE |
| 8 | QA Agent | Sonnet | qa-agent.md | NOT DEFINED |
| 9 | DevOps | Sonnet | devops.md | NOT DEFINED |

## Process Order

```
Product Owner (James)
    → Technology Analyst — research, evaluation, tech decisions
    → Product Manager — plans what to build, designs approach
    → Business Analyst — formalizes requirements, success criteria
    → Project Manager — tracks state, progress, docs throughout
    → Developer — writes the code
    → Tester — writes and runs tests including performance
    → Security — vulnerability scanning
    → QA Agent — tests running app in browser
    → DevOps — CI/CD, branching, releases, environments
```

## Agents Being Retired

| Old Agent | Disposition |
|-----------|------------|
| Context Keeper | Absorbed into Project Manager |
| Planner | Absorbed into Product Manager |
| Implementer | Renamed to Developer |
| Validator | Responsibilities split to Tester + Security |
| CI/CD | Absorbed into DevOps |
| Code Scaffolder | Absorbed into Developer |
| Code Reviewer | Eliminated — covered by Tester + Security |
| Status Updater | Absorbed into Project Manager |
| Changelog Writer | Absorbed into Project Manager |
| Doc Generator | Absorbed into Project Manager |
| Recruiter | Eliminated — becomes orchestrator workflow |

## Files to Delete After New Definitions Complete

- context-keeper.md
- planner.md
- implementer.md
- validator.md
- cicd.md
