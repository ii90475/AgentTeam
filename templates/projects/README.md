# Project Templates

Templates for different project archetypes, used by the Recruiter Agent to scaffold new projects.

## Available Templates

| Template | Description | Best For |
|----------|-------------|----------|
| [web-app](web-app.md) | Full-stack web application | SaaS, dashboards, portals |
| [api-service](api-service.md) | Backend API service | Microservices, integrations |
| [mobile-app](mobile-app.md) | iOS/Android application | Consumer apps, mobile-first products |
| [cli-tool](cli-tool.md) | Command-line interface | Dev tools, automation, utilities |
| [marketing-content](marketing-content.md) | Marketing/content sites | Landing pages, blogs, docs sites |
| [data-ml](data-ml.md) | Data/ML pipelines | Analytics, ML models, ETL |
| [library-package](library-package.md) | Reusable library | npm/PyPI packages, SDKs |

## Template Structure

Each template includes:
- **Description** — What this project type is
- **Tech Stack Options** — Common choices for each layer
- **Recommended Agents** — Which local and Claude agents to use
- **Project Structure** — Directory layout
- **Setup Checklist** — Initial configuration steps

## Adding New Templates

1. Create `{template-name}.md` in this folder
2. Follow the existing template format
3. Update this README with the new entry
4. The Recruiter Agent will automatically recognize it

## Customization

Templates are starting points. The Recruiter Agent may:
- Combine templates (e.g., web-app + api-service for monorepo)
- Adapt structure based on user preferences
- Skip irrelevant sections based on project scope
