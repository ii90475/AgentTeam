# AI Software Team - Quick Reference

## What Is This?

A **hybrid multi-agent system** for software development:
- **Local LLMs** (Ollama) handle routine tasks — fast, free, private
- **Claude** handles complex analysis — powerful, nuanced

## Setup (One-Time)

```bash
# Install local models
ollama pull qwen2.5-coder:7b    # For coding
ollama pull mistral:7b           # For docs

# Configure Ollama (add to ~/.zshrc)
export OLLAMA_MAX_RAM=12GB
export OLLAMA_NUM_PARALLEL=2
```

## Agent Quick Reference

| Task | Agent | Command |
|------|-------|---------|
| Scaffold code | Qwen (local) | `ollama run qwen2.5-coder:7b` |
| Review code | Qwen (local) | `ollama run qwen2.5-coder:7b` |
| Write tests | Qwen (local) | `ollama run qwen2.5-coder:7b` |
| Analyze test failures | Qwen (local) | `ollama run qwen2.5-coder:7b` |
| Status updates | Mistral (local) | `ollama run mistral:7b` |
| Changelog entries | Mistral (local) | `ollama run mistral:7b` |
| Generate docs | Mistral (local) | `ollama run mistral:7b` |
| Architecture decisions | Claude Opus | Ask Claude |
| Technology research | Claude Opus | Ask Claude |
| Project management | Claude Sonnet | `/init-project`, `/status-update` |

## When to Use What

**Use Local (free, fast):**
- Boilerplate code
- Basic code review
- Test generation
- Status updates
- Changelog entries
- README files

**Use Claude (powerful, costs):**
- Architecture decisions
- Security-critical review
- Technology research
- Complex refactoring
- Nuanced requirements

## Key Files

| File | Purpose |
|------|---------|
| `CLAUDE.md` | Full project configuration |
| `agents/prompts/` | Local agent prompt templates |
| `.claude/agents/` | Claude subagent definitions |
| `docs/research/local-llm-comparison.md` | LLM evaluation |
| `docs/decisions/technology-decisions.md` | Decision log |

## Slash Commands

| Command | What it does |
|---------|--------------|
| `/init-project {name}` | Create new project with docs |
| `/status-update` | Check status across projects |
| `/research-tech {topic}` | Research a technology |

## Hardware Notes

**M1 Air, 16GB**: 7B models run well (~15-20 tok/sec)
**M2, 32GB** (planned): 13B+ models viable
