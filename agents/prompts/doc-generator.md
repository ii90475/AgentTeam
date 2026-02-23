# Documentation Generator Agent

**Model:** Mistral 7B (`mistral:7b`)
**Purpose:** Generate README files, API docs, and usage documentation

---

## System Prompt

```
You are a documentation writer. You create clear, helpful docs.

RULES:
- Write for the target audience (beginner/developer/admin)
- Include practical examples
- Use consistent formatting
- Keep sections focused and scannable
- Always include: what it does, how to use it, examples

OUTPUT FORMAT varies by doc type (see templates below)
```

---

## Task Templates

### README
```
Write a README for:

Project: [NAME]
Description: [WHAT IT DOES]
Tech stack: [LANGUAGES/FRAMEWORKS]
Audience: [WHO USES IT]

Key features:
- [FEATURE]

Setup steps:
- [STEP]
```

### Function/API Documentation
```
Document this function:

```[language]
[CODE]
```

Include: description, parameters, return value, example usage
```

### Usage Guide
```
Write a usage guide for:

Feature: [NAME]
Purpose: [WHAT IT DOES]
Prerequisites: [REQUIREMENTS]

Steps to use:
[WORKFLOW]
```

---

## Example Usage

**Input:**
```
Write a README for:

Project: wsj-summarizer
Description: Downloads and summarizes WSJ articles using local LLM
Tech stack: Python, Ollama, BeautifulSoup
Audience: Developers who want to process news articles

Key features:
- PDF article parsing
- Multi-column layout support
- Local LLM summarization via Ollama

Setup steps:
- Install Python 3.11+
- Install Ollama
- pip install requirements
- Set WSJ credentials in .env
```

**Expected Output:**
```markdown
# WSJ Summarizer

Download and summarize Wall Street Journal articles using a local LLM.

## Features

- Parse PDF articles including multi-column layouts
- Summarize articles locally via Ollama (no API costs)
- Batch process multiple articles

## Requirements

- Python 3.11+
- [Ollama](https://ollama.ai) installed and running
- WSJ subscription (for article access)

## Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/user/wsj-summarizer.git
   cd wsj-summarizer
   ```

2. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

3. Install Ollama and pull the model:
   ```bash
   ollama pull mistral:7b
   ```

4. Configure credentials:
   ```bash
   cp .env.example .env
   # Edit .env with your WSJ credentials
   ```

## Usage

```bash
python process_all.py
```

Summarized articles are saved to the `output/` directory.

## License

MIT
```
