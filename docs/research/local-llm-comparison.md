# Local LLM Comparison for M1 MacBook Air (16GB)

**Date:** 2025-01-19
**Purpose:** Select optimal local LLMs for hybrid agent architecture
**Hardware:** M1 MacBook Air, 16GB RAM, Ollama 0.14.2

---

## Executive Summary

For an M1 MacBook Air with 16GB RAM, **7B parameter models** are the practical maximum for responsive performance. Larger models (13B+) will run but with noticeable slowdowns and thermal throttling.

### Recommendations

| Use Case | Model | Install Command |
|----------|-------|-----------------|
| **Coding tasks** | Qwen 2.5 Coder 7B | `ollama pull qwen2.5-coder:7b` |
| **General/Docs** | Mistral 7B | `ollama pull mistral:7b` |
| **Lightweight tasks** | Phi-3 Mini | `ollama pull phi3:mini` |
| **Reasoning** | DeepSeek R1 7B | `ollama pull deepseek-r1:7b` |

---

## Hardware Constraints

### M1 MacBook Air with 16GB RAM

| Model Size | Performance | Recommendation |
|------------|-------------|----------------|
| 3B | ~25-30 tokens/sec | Excellent |
| 7B | ~15-20 tokens/sec | Good (optimal) |
| 13B | ~8-12 tokens/sec | Slow, thermal throttling |
| 30B+ | <5 tokens/sec | Not practical |

**Key considerations:**
- MacBook Air has passive cooling (no fan) — sustained inference causes thermal throttling
- RAM usage: Reserve ~4GB for system, leaving ~12GB for model
- Quantization helps: Q4 versions use ~4GB for 7B models

### Future Hardware: M2 with 32GB

With 32GB, you could comfortably run:
- 13B models at good speeds
- 30B quantized models (slower but usable)
- Multiple smaller models loaded simultaneously

---

## Model Evaluations

### Coding: Qwen 2.5 Coder 7B (Recommended)

**Strengths:**
- 85%+ HumanEval benchmark (matches GitHub Copilot level)
- Supports 92 programming languages
- Excellent at code completion, debugging, refactoring
- Strong at following structured prompts

**Weaknesses:**
- Worse at general knowledge tasks (trained heavily on code/math)
- Can hallucinate on non-technical topics

**Memory:** ~4.5GB (Q4 quantized)

**Best for:** Code scaffolding, boilerplate generation, code review assistance

```bash
ollama pull qwen2.5-coder:7b
```

---

### General Purpose: Mistral 7B (Recommended)

**Strengths:**
- Best balance of speed and capability at 7B
- Reliable, consistent outputs
- Efficient memory usage
- Good instruction following

**Weaknesses:**
- Not specialized for any particular domain
- Weaker than Qwen on pure coding tasks

**Memory:** ~4GB (Q4 quantized)

**Best for:** Status updates, changelog entries, documentation, general assistance

```bash
ollama pull mistral:7b
```

---

### Alternative: Llama 3.2 7B

**Strengths:**
- Strong general capabilities
- Good at documentation and technical writing
- Well-supported ecosystem

**Weaknesses:**
- Slightly slower than Mistral on M1
- Requires more memory

**Best for:** If you prefer Meta's ecosystem or need better long-form writing

```bash
ollama pull llama3.2:7b
```

---

### Lightweight: Phi-3 Mini (2.7B)

**Strengths:**
- Very fast (~30+ tokens/sec)
- Surprisingly capable for size
- Minimal resource usage

**Weaknesses:**
- Limited on complex tasks
- Smaller context window

**Best for:** Quick templated tasks, simple completions, when speed matters most

```bash
ollama pull phi3:mini
```

---

### Reasoning: DeepSeek R1 7B

**Strengths:**
- Shows step-by-step reasoning
- Good at complex problem solving
- Strong math capabilities

**Weaknesses:**
- Slower due to reasoning tokens
- Verbose outputs

**Best for:** When you need transparent reasoning for debugging or complex logic

```bash
ollama pull deepseek-r1:7b
```

---

## Benchmark Comparison

| Model | HumanEval | MBPP | Speed (M1) | Memory |
|-------|-----------|------|------------|--------|
| Qwen 2.5 Coder 7B | 85%+ | ~70% | ~15 t/s | 4.5GB |
| Mistral 7B | ~35% | ~45% | ~18 t/s | 4GB |
| CodeLlama 7B | 33.5% | 41.8% | ~15 t/s | 4GB |
| Llama 3.2 7B | ~40% | ~50% | ~14 t/s | 4.5GB |
| Phi-3 Mini | ~30% | ~40% | ~30 t/s | 2GB |

---

## Recommended Setup

### Install Commands

```bash
# Primary models for hybrid architecture
ollama pull qwen2.5-coder:7b    # For coding tasks
ollama pull mistral:7b           # For docs/general tasks

# Optional additions
ollama pull phi3:mini            # For quick/simple tasks
ollama pull deepseek-r1:7b       # For reasoning tasks
```

### Ollama Configuration

For optimal performance on 16GB M1:

```bash
# Set in ~/.zshrc or ~/.bashrc
export OLLAMA_MAX_RAM=12GB
export OLLAMA_NUM_PARALLEL=2
```

---

## Hybrid Architecture Mapping

| Task Type | Local Model | When to Use Claude |
|-----------|-------------|-------------------|
| Status updates | Mistral 7B | Complex project analysis |
| Changelog entries | Mistral 7B | Major release summaries |
| Code scaffolding | Qwen 2.5 Coder | Complex architecture decisions |
| Boilerplate | Qwen 2.5 Coder | Novel patterns/integrations |
| README generation | Mistral 7B | Marketing-quality docs |
| Code review | Qwen 2.5 Coder | Security audits, complex logic |
| Quick questions | Phi-3 Mini | N/A |

---

## Sources

- [Best Local LLMs for Apple Silicon](https://apxml.com/posts/best-local-llm-apple-silicon-mac)
- [Ollama on Mac Silicon Guide](https://johnwlittle.com/ollama-on-mac-silicon-local-ai-for-m-series-macs/)
- [Best Ollama Models for Coding 2025](https://www.codegpt.co/blog/choosing-best-ollama-model)
- [Comparing Open-Source AI Models](https://www.ankursnewsletter.com/p/comparing-open-source-ai-models-llama)
- [Best Ollama Models Performance Guide](https://collabnix.com/best-ollama-models-in-2025-complete-performance-comparison/)
- [Running LLM Locally on M1](https://medium.com/@dlaytonj2/can-you-run-a-large-language-model-llm-locally-on-an-m1-macbook-air-with-only-16-gb-of-memory-cd9741af27bb)

---

## Next Steps

1. Install recommended models via Ollama
2. Test each model on sample tasks from your projects
3. Design agent prompts optimized for these models' strengths
4. Build evaluation framework to measure quality vs. Claude baseline
