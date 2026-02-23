# Library/Package Template

## Description
Reusable code library or package published to a package registry (npm, PyPI, crates.io, etc.).

## Typical Tech Stacks

| Layer | Options |
|-------|---------|
| Language | TypeScript, Python, Rust, Go |
| Build | tsup, rollup, setuptools, cargo |
| Testing | Jest, Vitest, pytest, cargo test |
| Docs | TypeDoc, Sphinx, rustdoc |
| Registry | npm, PyPI, crates.io |
| CI | GitHub Actions |

## Recommended Agents

### Local Agents (Routine Tasks)
| Agent | Use For |
|-------|---------|
| **code-scaffolder** | Functions, classes, modules |
| **code-reviewer** | API design, edge cases |
| **test-builder** | Unit tests, edge case coverage |
| **test-runner** | Debug test failures |
| **doc-generator** | API docs, usage examples |
| **changelog-writer** | Version release notes |

### Claude Agents (Complex Tasks)
| Agent | Use For |
|-------|---------|
| **project-manager** | Release planning, semver decisions |
| **technology-analyst** | API design, compatibility |

## Project Structure

```
{project-name}/
├── .claude/
├── CLAUDE.md
├── README.md
├── docs/
│   ├── api-reference.md
│   ├── getting-started.md
│   └── changelog.md
├── src/
│   ├── index.ts         # Entry point / exports
│   ├── core/            # Core functionality
│   ├── utils/           # Internal helpers
│   └── types/           # Type definitions
├── tests/
│   ├── unit/
│   └── integration/
├── examples/
│   └── basic-usage/
├── .env.example
├── .gitignore
├── package.json / pyproject.toml / Cargo.toml
├── tsconfig.json (if TS)
└── LICENSE
```

## Initial Setup Checklist

- [ ] Initialize git repository
- [ ] Set up build tooling
- [ ] Configure TypeScript/linting
- [ ] Design public API surface
- [ ] Write comprehensive tests
- [ ] Create usage examples
- [ ] Generate API documentation
- [ ] Set up CI for tests and publishing
- [ ] Configure semantic versioning
- [ ] Write CONTRIBUTING guide
- [ ] Choose and add LICENSE
- [ ] Publish initial version
