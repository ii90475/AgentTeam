# Decision: Team Restructure v4.0.0

**Date:** 2026-03-11
**Decision by:** Product Owner

## Context

Previous team had 18 agents defined in CLAUDE.md but only 7 behavioral definitions existed. Many agents had redundant responsibilities. Team was over-engineered with made-up titles (e.g., "Context Keeper") that don't exist in real-world software teams.

## Decision

Reduce to 9 agents with real-world titles and clear, non-overlapping areas of responsibility.

## Agents Retired

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
| Test Builder | Merged into Tester |
| Test Runner | Merged into Tester |

## New Team

| # | Role | Model Tier |
|---|------|-----------|
| 1 | Technology Analyst | Best available |
| 2 | Product Manager | Second best available |
| 3 | Business Analyst | Best available |
| 4 | Project Manager | Best available |
| 5 | Developer | Second best available |
| 6 | Tester | Most efficient available |
| 7 | Security | Second best available |
| 8 | QA Agent | Second best available |
| 9 | DevOps | Second best available |

## Rationale

- Right-sized team of specialists with no redundancy
- Real-world titles that map to industry roles
- Clear process order with defined handoffs
- Independence where it matters: Tester, Security, QA test Developer's work independently
- PM drives sprints autonomously — reduces PO bottleneck for long-running work
- FailPoints resolution process built into PM and Project Manager roles for continuous improvement
