# Agent Prompts

Optimized prompts for local LLM agents running on M1 MacBook Air (16GB).

## Agent Inventory

| Agent | Model | Purpose |
|-------|-------|---------|
| [code-scaffolder](code-scaffolder.md) | Qwen 2.5 Coder 7B | Generate boilerplate code |
| [code-reviewer](code-reviewer.md) | Qwen 2.5 Coder 7B | Review code for issues |
| [test-builder](test-builder.md) | Qwen 2.5 Coder 7B | Generate test suites |
| [test-runner](test-runner.md) | Qwen 2.5 Coder 7B | Analyze test failures |
| [status-updater](status-updater.md) | Mistral 7B | Write session status updates |
| [changelog-writer](changelog-writer.md) | Mistral 7B | Generate changelog entries |
| [doc-generator](doc-generator.md) | Mistral 7B | Create documentation |

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

## When to Escalate to Claude

Use Claude instead of local models for:

- Complex architecture decisions
- Security-critical code review
- Nuanced requirements interpretation
- Multi-file refactoring with dependencies
- Research and technology evaluation

## Adding New Agents

1. Create `agents/prompts/[agent-name].md`
2. Follow the template structure:
   - Header with model and purpose
   - System prompt in code block
   - Task templates
   - Example usage with expected output
3. Test with representative tasks
4. Add to inventory table above
