# Requirements: Agent Team

## Scope
In scope: Agent system design, agent definitions, evaluation criteria, workflow, templates
Out of scope: Individual project implementations

## Requirements

### REQ-001: QA Agent — Browser-Based E2E Testing
- Description: Agent that tests running web applications using Playwright, judges behavioral correctness against BA requirements
- Success criteria: Can generate test plans from requirements, execute browser tests, capture evidence, approve/reject deliverables
- Priority: Must
- Status: Done (v2.0.0)

### REQ-002: Configurable QA Approval Mode
- Description: QA approval authority configurable per project — recommend (user reviews) or autonomous (QA PASS is final gate)
- Success criteria: qa-config.md supports approval_mode setting, QA Agent branches behavior accordingly
- Priority: Must
- Status: Done (v2.0.0)

### REQ-003: CLAUDE.md Rules Rework
- Description: Trim over-engineered sections (4D Framework, Interaction Modes, Session Opener, Feedback Shortcuts), keep core rules
- Success criteria: ~/AI/CLAUDE.md reduced from ~320 lines to ~120 lines. Every remaining line serves: accuracy, honesty, verified outputs, clarity, security, no showing off.
- Priority: Must
- Status: Done (v3.0.0)

### REQ-004: QA Agent Real-World Validation
- Description: Test QA Agent against an actual web-app project to validate end-to-end workflow
- Success criteria: /run-qa successfully generates test plan, executes Playwright tests, produces evidence-based verdict
- Priority: Should
- Status: Pending

### REQ-005: Unified Claude Subagent Architecture
- Description: Convert all 18 agents to Claude Code subagents with process isolation. Main session becomes orchestrator only. Configurable Ollama lite mode retained for offline/prototyping.
- Success criteria: 18 subagent files in .claude/agents/ with YAML frontmatter. Agents cannot see each other's reasoning. Orchestrator protocol documented. Engine config per project (claude/ollama). Ollama limitations documented with gap-closing strategies.
- Priority: Must
- Status: Done (v3.0.0)

### REQ-006: Ollama Limitations Documentation
- Description: Document what 7B models can and cannot do, quality comparison per agent, when to use Ollama, gap-closing strategies.
- Success criteria: docs/ollama-limitations.md exists with actionable guidance. docs/engine-configuration.md explains how to configure per project.
- Priority: Must
- Status: Done (v3.0.0)
