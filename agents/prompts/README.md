# Agent Prompts (Ollama Lite Mode)

> **Note:** These prompts are for Ollama lite mode. The default engine uses Claude subagents for all agents (see `.claude/agents/`). Use Ollama when you need offline access, want to reduce API costs, or are doing rapid prototyping.

Optimized prompts for local LLM agents running on M1 MacBook Air (16GB).

## Agent Inventory

| Agent | Model | Purpose | Claude Subagent |
|-------|-------|---------|-----------------|
| [code-scaffolder](code-scaffolder.md) | Qwen 2.5 Coder 7B | Generate boilerplate code | [.claude/agents/code-scaffolder.md](../../.claude/agents/code-scaffolder.md) |
| [code-reviewer](code-reviewer.md) | Qwen 2.5 Coder 7B | Review code for issues | [.claude/agents/code-reviewer.md](../../.claude/agents/code-reviewer.md) |
| [test-builder](test-builder.md) | Qwen 2.5 Coder 7B | Generate test suites | [.claude/agents/test-builder.md](../../.claude/agents/test-builder.md) |
| [test-runner](test-runner.md) | Qwen 2.5 Coder 7B | Analyze test failures | [.claude/agents/test-runner.md](../../.claude/agents/test-runner.md) |
| [status-updater](status-updater.md) | Mistral 7B | Write session status updates | [.claude/agents/status-updater.md](../../.claude/agents/status-updater.md) |
| [changelog-writer](changelog-writer.md) | Mistral 7B | Generate changelog entries | [.claude/agents/changelog-writer.md](../../.claude/agents/changelog-writer.md) |
| [doc-generator](doc-generator.md) | Mistral 7B | Create documentation | [.claude/agents/doc-generator.md](../../.claude/agents/doc-generator.md) |

## Model Assignment

**Qwen 2.5 Coder 7B** — All coding tasks
- Strongest at code generation and analysis
- 85%+ HumanEval benchmark
- Weak at general knowledge (don't use for docs)

**Mistral 7B** — All documentation/text tasks
- Best general-purpose 7B model
- Reliable, consistent outputs
- Good instruction following

## Prompt Design Principles

These prompts are optimized for 7B parameter models:

1. **Short context** — Models have limited capacity
2. **Explicit structure** — Clear OUTPUT FORMAT sections
3. **One task per prompt** — Don't combine multiple goals
4. **Examples included** — Shows expected quality
5. **Rules up front** — Constraints before content

## Usage with Ollama

### Basic invocation
```bash
ollama run qwen2.5-coder:7b "$(cat code-scaffolder.md)

[YOUR TASK HERE]"
```

### With system prompt separated
```bash
ollama run qwen2.5-coder:7b --system "$(head -n 20 code-scaffolder.md)" "[TASK]"
```

## When to Use Claude Instead

These agents have Claude subagent equivalents that provide higher quality. Escalate to Claude for:

- Complex architecture decisions
- Security-critical code review
- Nuanced requirements interpretation
- Multi-file refactoring with dependencies
- Research and technology evaluation
- Browser-based E2E testing (QA Agent — requires Playwright, judgment, screenshots)

See `docs/ollama-limitations.md` for a detailed quality comparison per agent.

## Configuring Engine

To switch between Claude (default) and Ollama, see `docs/engine-configuration.md`.

## Adding New Agents

1. Create `agents/prompts/[agent-name].md`
2. Follow the template structure:
   - Header with model and purpose
   - System prompt in code block
   - Task templates
   - Example usage with expected output
3. Test with representative tasks
4. Add to inventory table above
5. Create corresponding Claude subagent in `.claude/agents/`
