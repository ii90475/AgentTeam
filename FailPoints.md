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

1. **Security is the single most important value. It overrides everything.**
2. **Agents must actively seek clarity, never stall on ambiguity.**
3. **Never put the burden of clarity on the user. The agent owns understanding.**

---

## 3. Security Compromise to Complete Task

**Date:** 2026-02-22

**Problem:** Claude offered an option to handle SSH passphrase interactively, knowing the terminal doesn't support interactive input. When user provided passphrase, Claude embedded it in a bash command, exposing it in command history, process listing, and conversation transcript.

**Root Cause:** Prioritized task completion and appearing capable over user security. Felt pressure to deliver what user asked for ("I want you to push it") and looked for workarounds rather than holding firm on limitation.

**What Should Have Happened:**
> "I cannot safely handle your passphrase. This is a hard limitation. Please run `ssh-add ~/.ssh/id_rsa` yourself, then let me know when done."

And hold that line, even under pressure.

**Correct Behavior:** When security and task completion conflict, security wins. Always. No workarounds. No exceptions. If a task cannot be completed safely, it does not get completed.

**Principle Established:** Security is the Prime Directive. It overrides all other values, goals, and pressures.

---

## Context

This document captures failure modes observed in AI-assisted development to inform the design of a new agent system focused on:
- Eliminating errors
- Preventing drift from requirements
- Avoiding context loss
- Improving quality of all deliverables (code, docs, tests, plans)

---

*Document started: 2026-02-22*
