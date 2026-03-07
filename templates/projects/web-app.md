# Web Application Template

## Description
Full-stack web application with frontend, backend API, and database.

## Typical Tech Stacks

| Layer | Options |
|-------|---------|
| Frontend | React, Vue, Next.js, SvelteKit |
| Backend | Node/Express, Python/FastAPI, Go |
| Database | PostgreSQL, MongoDB, SQLite |
| Auth | NextAuth, Auth0, Clerk, custom JWT |
| Hosting | Vercel, Railway, AWS, self-hosted |

## Recommended Agents

All agents run as Claude subagents with process isolation. Ollama lite mode available for utility agents (see `docs/engine-configuration.md`).

| Agent | Model | Use For |
|-------|-------|---------|
| **context-keeper** | Sonnet | Session state, memory, agent monitoring |
| **business-analyst** | Sonnet | Requirements, scope, success criteria |
| **planner** | Sonnet | Implementation options, approval gate |
| **implementer** | Sonnet | Code execution, stops on ambiguity |
| **validator** | Sonnet | Quality gate, coordinates security + CI/CD |
| **security** | Sonnet | Vulnerability scanning, OWASP checks |
| **cicd** | Sonnet | Pipeline validation, deployment safety |
| **qa-agent** | Sonnet | Browser-based E2E testing against requirements |
| **code-scaffolder** | Haiku | Components, API endpoints, data models |
| **code-reviewer** | Sonnet | PR reviews, security checks |
| **test-builder** | Haiku | Unit tests, integration tests |
| **test-runner** | Haiku | Analyze test failures |
| **doc-generator** | Haiku | README, API docs |
| **changelog-writer** | Haiku | Release notes |
| **status-updater** | Haiku | Session logs |
| **project-manager** | Sonnet | Planning, milestones, progress tracking |
| **technology-analyst** | Opus | Tech stack decisions, architecture |

## Project Structure

```
{project-name}/
├── .claude/
│   └── (symlink to agent configs)
├── CLAUDE.md
├── README.md
├── docs/
│   ├── architecture.md
│   ├── project-status.md
│   └── changelog.md
├── src/
│   ├── components/      # Frontend components
│   ├── pages/           # Routes/pages
│   ├── api/             # Backend API
│   ├── lib/             # Shared utilities
│   └── types/           # TypeScript types
├── tests/
│   ├── unit/
│   ├── integration/
│   └── e2e/                  # Playwright E2E tests (QA Agent)
├── .env.example
├── .gitignore
└── package.json (or requirements.txt, go.mod, etc.)
```

## Initial Setup Checklist

- [ ] Initialize git repository
- [ ] Set up package manager (npm/yarn/pnpm)
- [ ] Configure linting and formatting
- [ ] Set up testing framework
- [ ] Create .env.example with required variables
- [ ] Initialize database schema
- [ ] Install Playwright: `npx playwright install`
- [ ] Create QA config: `docs/projects/{project}/state/qa-config.md`
- [ ] Set up CI/CD pipeline
