# Decisions Log: Agent Team

## 2026-03-07: QA Agent Design Decisions

| Decision | Choice | Rationale | Role |
|----------|--------|-----------|------|
| QA Agent hierarchy position | Peer of Validator, runs after | Different scope (code-level vs application-level), no point running browser tests on broken code | Planner |
| QA Agent model | Sonnet | Sufficient for structured test execution; ambiguous results escalate to user, not bigger model | Technology Analyst |
| Browser automation tool | Playwright | Better cross-browser, better async, actively maintained by Microsoft | Technology Analyst |
| Approval authority | Configurable per project (recommend/autonomous) | Some projects require user review, some don't; user review is default | User |
| Application startup | QA Agent never starts the app | Environment-specific concerns outside QA scope; only tests what's running | Planner |
| Test plan persistence | Yes, in docs/projects/{project}/qa/ | Traceability, auditability, prevents inventing tests at runtime | Planner |

## 2026-03-07: v3.0.0 Architecture Decisions

| Decision | Choice | Rationale | Role |
|----------|--------|-----------|------|
| Agent execution model | All 18 as Claude subagents with process isolation | Definition agents had no real separation — Claude played all roles in single context | User + Context Keeper |
| Ollama disposition | Retained as configurable lite mode, not removed | Still useful for offline/cost-sensitive work; zero invocations but has valid use cases | User |
| Model tier: Opus | technology-analyst only | Deep multi-criteria reasoning with web research justifies cost | Technology Analyst |
| Model tier: Sonnet | 11 judgment agents (workflow + code-reviewer + recruiter + PM) | Judgment-requiring work needs reasoning depth | Technology Analyst |
| Model tier: Haiku | 6 pattern-following agents (scaffolder, test-builder/runner, status, changelog, doc-gen) | Pattern-following, templated tasks — fast and cheap | Technology Analyst |
| code-reviewer model | Sonnet (not Haiku) | Code review requires genuine judgment, not just pattern matching | User |
| Orchestrator design | Main session coordinates only, no agent file | Orchestrator routes work but does not implement, validate, or evaluate | Planner |
| Agent communication | File-based handoffs (existing pattern) | Keeps auditability, prevents context contamination between agents | Planner |
| CLAUDE.md trim | Remove 4D Framework, Interaction Modes, Session Opener, Feedback Shortcuts, My Commitments | ~200 lines of ceremony that don't serve accuracy, honesty, or security | User |
| Command language | "Delegate to subagent" replaces "You are now acting as" | Commands should match actual architecture — delegation, not role-playing | Planner |

## 2026-03-07: CLAUDE.md Evaluation Findings

| Decision | Choice | Rationale | Role |
|----------|--------|-----------|------|
| Keep core rules | Security, Truth/Honesty, Verifiability, Clarity Protocol | Directly serve user requirements | User + Context Keeper |
| Rework checkpoint system | Needs mandatory testing gate, not just review pauses | Gap: no rule mandates verified outputs before delivery | Context Keeper |
| Trim framework overhead | 4D Framework, Interaction Modes, Session Opener, Feedback Shortcuts flagged for removal | Over-engineered, performative, doesn't earn its place under user standards | User |
