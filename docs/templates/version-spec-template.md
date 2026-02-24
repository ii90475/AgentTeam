# {Project Name} — Version {version}

**Date:** {YYYY-MM-DD}
**Status:** Draft | In Review | Approved | Released

---

## Use Cases
<!-- PO provides use cases. Tag with [new], [extends UC-XXX vX.X], or [changes UC-XXX vX.X]. -->
<!-- BA evaluates for gaps, conflicts, implicit requirements. -->

### UC-001: {Title} [new]
**As a** {user type}, **I want to** {action} **so that** {outcome}.

**Flow:**
1. {step}
2. {step}

**Error states:**
- {what can go wrong → what should happen}

---

## Requirements
<!-- BA produces this after evaluating use cases. -->
<!-- Tag with [new], [extends REQ-XXX vX.X], or [changes REQ-XXX vX.X]. -->

| ID | Requirement | Source | Priority | Tests | Status |
|----|-------------|--------|----------|-------|--------|
| REQ-001 | {requirement} [new] | UC-001 | Must/Should/Could | T-001, T-002 | Pending |

### BA Evaluation Notes

- **Gaps identified:** {what was missing from use cases}
- **Implicit requirements added:** {auth, validation, error handling, etc.}
- **Conflicts flagged:** {contradictions between requirements}
- **Changes to prior versions:** {what was extended or changed, and why}

---

## Scope

**In scope for this version:**
- {item}

**Out of scope:**
- {item}

---

## Implementation Plan
<!-- Planner produces this. Approved by user before Implementer acts. -->

| Phase | What | Requirements Covered | Depends On |
|-------|------|---------------------|------------|
| 1 | {deliverable} | REQ-001, REQ-002 | — |
| 2 | {deliverable} | REQ-003 | Phase 1 |

---

## Tests
<!-- Validator/Test Builder produce this. Linked from requirements. -->

| ID | Description | Type | Covers | Status |
|----|-------------|------|--------|--------|
| T-001 | {test description} | Unit/Integration/E2E | REQ-001 | Pending |
| T-002 | {test description} | Unit/Integration/E2E | REQ-001 | Pending |

---

## Release Notes
<!-- Generated at release. User-facing summary. -->

### What's New in {version}
- {feature/change, written for end users}

### Bug Fixes
- {fix description}

### Known Issues
- {known issue, if any}

---

*Maintained by: BA (requirements), Planner (implementation), Validator (tests), Context Keeper (release notes).*
