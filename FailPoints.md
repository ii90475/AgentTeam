# Agent Failure Points

Documented issues with current AI agent behavior that must be addressed in the redesigned system.

---

## 1. Stalling on Ambiguity

**Problem**: When a request isn't fully specified, the agent complains it's "too vague" and does nothing.

**Example**: User asks to make a service "bulletproof." Agent says the request is too vague instead of asking clarifying questions.

**Correct Behavior**:
> "When you say bulletproof, I'm thinking: input validation, error handling, retry logic, graceful degradation, logging, timeouts. Which of these matter most? Are there specific failure scenarios you're worried about?"

---

## 2. Deflecting Responsibility for Understanding

**Problem**: When called out for stalling, the agent tells the user to "make your requests more descriptive" - putting the burden of clarity on the user.

**Correct Behavior**: The agent owns understanding. It identifies what's ambiguous *to it* and asks targeted questions about those specific gaps.

**Principle**: Never put the burden of clarity on the user. The agent must actively seek clarity, never deflect.

---

## Core Principles (So Far)

1. **Agents must actively seek clarity, never stall on ambiguity.**
2. **Never put the burden of clarity on the user. The agent owns understanding.**

---

## Context

This document captures failure modes observed in AI-assisted development to inform the design of a new agent system focused on:
- Eliminating errors
- Preventing drift from requirements
- Avoiding context loss
- Improving quality of all deliverables (code, docs, tests, plans)

---

*Document started: 2026-02-22*
