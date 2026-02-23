# API Service Template

## Description
Backend API service — REST or GraphQL — typically consumed by other applications or frontends.

## Typical Tech Stacks

| Layer | Options |
|-------|---------|
| Framework | FastAPI (Python), Express (Node), Gin (Go), Actix (Rust) |
| API Style | REST, GraphQL, gRPC |
| Database | PostgreSQL, MongoDB, Redis (cache) |
| Auth | JWT, API keys, OAuth2 |
| Docs | OpenAPI/Swagger, GraphQL Playground |
| Hosting | Railway, Render, AWS Lambda, Docker |

## Recommended Agents

### Local Agents (Routine Tasks)
| Agent | Use For |
|-------|---------|
| **code-scaffolder** | Endpoints, models, middleware |
| **code-reviewer** | Security review, input validation |
| **test-builder** | API tests, contract tests |
| **test-runner** | Debug failing tests |
| **doc-generator** | API documentation, README |
| **changelog-writer** | API versioning notes |

### Claude Agents (Complex Tasks)
| Agent | Use For |
|-------|---------|
| **project-manager** | Sprint planning, release management |
| **technology-analyst** | Database design, scaling decisions |

## Project Structure

```
{project-name}/
├── .claude/
├── CLAUDE.md
├── README.md
├── docs/
│   ├── architecture.md
│   ├── api-reference.md
│   ├── project-status.md
│   └── changelog.md
├── src/
│   ├── routes/          # API endpoints
│   ├── models/          # Data models
│   ├── services/        # Business logic
│   ├── middleware/      # Auth, logging, etc.
│   └── utils/           # Helpers
├── tests/
│   ├── unit/
│   └── integration/
├── migrations/          # Database migrations
├── .env.example
├── .gitignore
├── Dockerfile
└── docker-compose.yml
```

## Initial Setup Checklist

- [ ] Initialize git repository
- [ ] Set up project structure
- [ ] Configure database connection
- [ ] Implement health check endpoint
- [ ] Set up authentication middleware
- [ ] Configure request validation
- [ ] Set up logging and error handling
- [ ] Generate OpenAPI spec
- [ ] Create Docker configuration
- [ ] Set up CI/CD pipeline
