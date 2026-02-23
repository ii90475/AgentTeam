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

### Local Agents (Routine Tasks)
| Agent | Use For |
|-------|---------|
| **code-scaffolder** | Components, API endpoints, data models |
| **code-reviewer** | PR reviews, security checks |
| **test-builder** | Unit tests, integration tests |
| **test-runner** | Analyze test failures |
| **doc-generator** | README, API docs |
| **changelog-writer** | Release notes |
| **status-updater** | Session logs |

### Claude Agents (Complex Tasks)
| Agent | Use For |
|-------|---------|
| **project-manager** | Planning, milestones, progress tracking |
| **technology-analyst** | Tech stack decisions, architecture |

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
│   └── integration/
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
- [ ] Set up CI/CD pipeline
