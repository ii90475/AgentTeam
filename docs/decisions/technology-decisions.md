# Technology Decision Log

Centralized record of technology choices across all projects.

## Active Decisions

### Hybrid LLM Architecture
- **Date**: 2025-01-19
- **Projects Affected**: All projects using AI Software Team
- **Decision**: Use hybrid architecture combining local LLMs (Ollama) for routine tasks with Claude API for complex analysis
- **Rationale**:
  - Cost efficiency: No API costs for routine, high-volume tasks
  - Speed: Local inference eliminates network latency
  - Privacy: Code and data stay local for routine processing
  - Quality: Claude handles nuanced, complex decisions where local models fall short
- **Research Report**: [Local LLM Comparison](../research/local-llm-comparison.md)
- **Status**: active

### Local LLM Selection
- **Date**: 2025-01-19
- **Projects Affected**: All projects using AI Software Team
- **Decision**:
  - **Coding tasks**: Qwen 2.5 Coder 7B
  - **Documentation/general**: Mistral 7B
- **Rationale**:
  - Qwen 2.5 Coder: 85%+ HumanEval benchmark, 92 language support, but weak at general knowledge
  - Mistral 7B: Best balance of speed and quality at 7B, reliable instruction following
  - Both run well on M1 MacBook Air with 16GB (~15-20 tokens/sec)
- **Research Report**: [Local LLM Comparison](../research/local-llm-comparison.md)
- **Status**: active

---

## Default Stack Preferences

| Component | Preferred Technology | Alternatives | Notes |
|-----------|---------------------|--------------|-------|
| Local LLM (Code) | Qwen 2.5 Coder 7B | CodeLlama 7B, DeepSeek Coder | Best HumanEval scores |
| Local LLM (Docs) | Mistral 7B | Llama 3.2 7B | Most reliable at 7B |
| Local LLM Runtime | Ollama | LM Studio | Simpler CLI, good Mac support |
| Complex Analysis | Claude Opus | Claude Sonnet | Use Opus for architecture/research |
| Routine Claude Tasks | Claude Sonnet | Claude Haiku | Balance of speed and quality |
| Frontend Framework | | | |
| Backend Framework | | | |
| Database | | | |
| Hosting | | | |
| Authentication | | | |
| Payments | | | |
| Email | | | |
| Object Storage | | | |

---

## Decision Template

When adding new decisions, use this format:

### {Decision Title}
- **Date**: {YYYY-MM-DD}
- **Projects Affected**: {list of projects}
- **Decision**: {what was decided}
- **Rationale**: {why}
- **Research Report**: {link to detailed report if exists}
- **Status**: {active|deprecated|under-review}

---
*Maintained by: Technology Analyst Agent*
