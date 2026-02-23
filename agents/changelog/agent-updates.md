# Agent Updates Changelog

## Purpose

Track all changes to agent definitions. Links failures to improvements.

## Format

Each entry includes:
- Agent affected
- Version change
- What changed
- Why (linked to FailPoints.md if applicable)
- Date

---

## Updates

### 2026-02-22

#### Context Keeper 1.0.0
- **Change:** Initial definition
- **Type:** Major (new agent)
- **Reason:** Agent team redesign based on BuildingBetterAgents.md
- **FailPoints Reference:** N/A - foundational

#### Context Keeper 1.1.0
- **Change:** Added context memory tracking, session start performance report, calendar-based periodic reviews, post-mortem deep dive structure
- **Type:** Minor (new capabilities)
- **Reason:** User feedback on review cadence and context loss prevention
- **FailPoints Reference:** Original pain points in BuildingBetterAgents.md about drift and context loss

#### Business Analyst 1.0.0
- **Change:** Initial definition
- **Type:** Major (new agent)
- **Reason:** Agent team redesign - owns requirements, scope, success criteria
- **FailPoints Reference:** N/A - foundational

#### Planner 1.0.0
- **Change:** Initial definition
- **Type:** Major (new agent)
- **Reason:** Agent team redesign - presents options, requires approval before action
- **FailPoints Reference:** N/A - foundational

#### Implementer 1.0.0
- **Change:** Initial definition
- **Type:** Major (new agent)
- **Reason:** Agent team redesign - minimal execution, stops on ambiguity
- **FailPoints Reference:** N/A - foundational

#### Validator 1.0.0
- **Change:** Initial definition
- **Type:** Major (new agent)
- **Reason:** Agent team redesign - validates output, coordinates subagents
- **FailPoints Reference:** N/A - foundational

#### Security 1.0.0
- **Change:** Initial definition
- **Type:** Major (new subagent)
- **Reason:** Agent team redesign - security scanning, OWASP, dependency audit
- **FailPoints Reference:** N/A - foundational

#### CI/CD 1.0.0
- **Change:** Initial definition
- **Type:** Major (new subagent)
- **Reason:** Agent team redesign - pipeline integrity, deployment safety
- **FailPoints Reference:** N/A - foundational

---

## Pending Updates

*Updates identified but not yet implemented*

| Agent | Proposed Change | Reason | Status |
|-------|-----------------|--------|--------|
| - | - | - | - |

---

## Update Process

1. Failure observed and documented in [FailPoints.md](../../FailPoints.md)
2. Triage with user to identify root cause
3. Determine which agent definition needs update
4. Draft change to agent definition
5. Review with user
6. Apply change, bump version
7. Log here with FailPoints reference
