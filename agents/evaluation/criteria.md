# Agent Evaluation Criteria

## Purpose

Define measurable criteria for evaluating agent performance. Used by Context Keeper for monitoring and by user for periodic review.

## Evaluation Framework

### Per-Agent Criteria

#### Context Keeper
| Indicator | Success | Failure |
|-----------|---------|---------|
| Session continuity | User understands current state immediately | User confused about where we left off |
| Performance report | Clear summary of agent/context health at session start | No report or incomplete report |
| Context memory | Drift and loss detected early, external state maintained | Context lost without warning |
| Failure detection | Issues raised before user notices | User discovers problems first |
| Agent monitoring | Violations caught and raised | Violations slip through |
| Documentation quality | FailPoints.md entries are actionable | Entries are vague or incomplete |
| Improvement loop | Agent prompts updated after failures | Same failures repeat |
| Review tracking | Periodic reviews triggered on schedule | Reviews missed or forgotten |

#### Business Analyst
| Indicator | Success | Failure |
|-----------|---------|---------|
| Requirements clarity | Implementable without ambiguity | Questions arise during implementation |
| Scope definition | Clear boundaries, in/out explicit | Scope creep occurs |
| Success criteria | Testable, measurable | Vague "it should work" |
| Completeness | All user needs captured | Missing requirements discovered late |
| Traceability | Every feature maps to requirement | Orphan features exist |

#### Planner
| Indicator | Success | Failure |
|-----------|---------|---------|
| Options presented | Multiple approaches with trade-offs | Single approach assumed |
| Approval obtained | Explicit user approval before action | Action taken without approval |
| Plan clarity | Implementer can execute without questions | Confusion during implementation |
| Minimal scope | Plan addresses only what's needed | Plan includes extras |
| Reasoning shown | User understands why recommendation made | Black box recommendation |

#### Implementer
| Indicator | Success | Failure |
|-----------|---------|---------|
| Plan adherence | Output matches approved plan exactly | Deviations or additions |
| Minimalism | No unnecessary code/content | Extras added "while we're here" |
| Ambiguity handling | Stops and asks when unclear | Assumes and proceeds |
| Verification | Claims are tested before stating | Untested claims made |
| Code quality | Commented, clean, functional | Uncommented, messy, broken |

#### Validator
| Indicator | Success | Failure |
|-----------|---------|---------|
| Issue detection | Problems found before delivery | User finds problems |
| Requirements match | Output verified against BA specs | Output drifts from specs |
| Test coverage | All requirement types tested | Gaps in testing |
| Values compliance | Output meets all stated values | Values violated |
| Scope check | No invented additions | Scope creep undetected |

#### Security (Subagent)
| Indicator | Success | Failure |
|-----------|---------|---------|
| Vulnerability detection | Issues found during development | Issues found in production |
| Dependency audit | Vulnerable dependencies flagged | Vulnerable dependencies shipped |
| OWASP compliance | Top 10 checked and addressed | Common vulnerabilities present |
| Auth/Authz | Access controls verified | Authorization gaps exist |

#### CI/CD (Subagent)
| Indicator | Success | Failure |
|-----------|---------|---------|
| Pipeline integrity | Builds are reliable and consistent | Flaky or broken builds |
| Deployment safety | Deployments are reversible and safe | Deployment causes outage |
| Environment parity | Dev/staging/prod aligned | Environment-specific bugs |
| Automation | Manual steps minimized | Manual intervention required |

## Cross-Agent Criteria

| Indicator | Success | Failure |
|-----------|---------|---------|
| Handoff clarity | Receiving agent has full context | Context lost in handoff |
| No duplication | Each agent does its job only | Agents overlap or redo work |
| Escalation | Issues raised to appropriate agent/user | Issues hidden or ignored |
| Values alignment | All agents uphold core values | Values violated anywhere |

## Review Cadence

| Review Type | Frequency | Trigger | Owner |
|-------------|-----------|---------|-------|
| Per-session | Every session start | Session begins | Context Keeper |
| Per-failure | As failures occur | Failure detected | Context Keeper + User |
| Periodic | Weekly | >7 days since last (calendar-based, not session-based) | Context Keeper + User |
| Post-mortem | After significant failures | Major failure or user request | User + All agents |

**Note:** Periodic reviews are tracked by calendar date in `state/last-review.md`, not by session count. Starting a new session does not reset the weekly clock.

### Per-Session Report Contents
- Agent health summary (recent failures, violations)
- Context health (drift, loss indicators)
- Pending issues requiring attention
- Time since last periodic review

### Post-Mortem Structure (Deep Dive)

| Element | Purpose |
|---------|---------|
| Timeline | What happened, when, sequence of events |
| Root cause | Why it happened - actual cause, not symptoms |
| Impact | What was affected, severity, scope |
| Agents involved | Which agents failed or contributed |
| Systemic issues | Patterns beyond this single instance |
| Prevention | Changes to prevent recurrence |
| Agent updates | Specific definition changes needed |

Post-mortem outputs:
1. FailPoints.md entry with full detail
2. Proposed agent definition updates
3. Systemic fixes if identified
4. Follow-up items for next session

## Scoring (Optional)

For periodic reviews, each criterion can be scored:

| Score | Meaning |
|-------|---------|
| 0 | Failure - criterion not met |
| 1 | Partial - some issues |
| 2 | Success - criterion fully met |

Aggregate scores identify which agents need definition updates.
