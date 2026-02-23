# CLI Tool Template

## Description
Command-line interface tool — utilities, dev tools, automation scripts.

## Typical Tech Stacks

| Layer | Options |
|-------|---------|
| Language | Python (Click, Typer), Node (Commander), Go (Cobra), Rust (Clap) |
| Config | YAML, TOML, JSON, dotenv |
| Distribution | pip, npm, brew, binary releases |
| Testing | pytest, Jest, go test |

## Recommended Agents

### Local Agents (Routine Tasks)
| Agent | Use For |
|-------|---------|
| **code-scaffolder** | Commands, subcommands, utilities |
| **code-reviewer** | Error handling, edge cases |
| **test-builder** | CLI integration tests |
| **doc-generator** | README, man pages, --help text |
| **changelog-writer** | Version release notes |

### Claude Agents (Complex Tasks)
| Agent | Use For |
|-------|---------|
| **project-manager** | Feature roadmap |
| **technology-analyst** | Distribution strategy |

## Project Structure

```
{project-name}/
├── .claude/
├── CLAUDE.md
├── README.md
├── docs/
│   ├── architecture.md
│   ├── usage.md
│   └── changelog.md
├── src/
│   ├── cli.py           # Entry point
│   ├── commands/        # Subcommands
│   ├── core/            # Business logic
│   └── utils/           # Helpers
├── tests/
│   ├── unit/
│   └── integration/
├── .env.example
├── .gitignore
├── setup.py / pyproject.toml / package.json
└── Makefile
```

## Initial Setup Checklist

- [ ] Initialize git repository
- [ ] Set up CLI framework (Click, Typer, etc.)
- [ ] Implement help text and version flag
- [ ] Add configuration file support
- [ ] Set up logging with verbosity levels
- [ ] Handle errors gracefully with helpful messages
- [ ] Add shell completion support
- [ ] Create installation instructions
- [ ] Set up release automation
- [ ] Publish to package registry
