# Claude Code Project Setup - PSB System Summary

Based on the video transcript in `setup.md`, this document captures the key takeaways from the PSB (Plan, Setup, Build) system for starting Claude Code projects.

---

## Phase 1: PLAN

### Two Questions to Ask Before Starting
1. **What are you actually trying to do?** (prototype, validate idea, build for production?)
2. **What are the milestones of functionality?** (MVP first, then iterations)

### Project Spec Doc (Two Parts)

**Product Requirements** (What & Why)
- Who is it for?
- What problems does it solve?
- What should the product do?
- Be specific about user interactions and workflows

**Engineering Requirements** (How)
- Tech stack choices (be explicit to avoid random choices)
- Technical architecture (system design, database schema, API design)
- Provision infrastructure early (databases, hosting, API keys)

### Using AI to Help Plan
- Tell AI to ask you questions to clarify requirements
- Use voice mode for fuzzy early-stage ideation
- Have AI summarize conversations into markdown specs

---

## Phase 2: SETUP (7-Step Checklist)

### 1. GitHub Repo Setup
- Enables Claude Code on web/mobile
- Access to GitHub CLI and Actions
- Deploy previews with Vercel
- Foundation for issue-based development

### 2. Create Environment Variable File (.env)
- Ask Claude to create example .env based on tech stack
- Fill in credentials so Claude doesn't stop to ask

### 3. CLAUDE.md File
Keep it focused. Include:
- Project goals and architecture overview
- Design style guide and UX guidelines
- Constraints and policies (e.g., "never push to main directly")
- Repository etiquette (PRs, branch naming)
- Frequently used commands
- Testing instructions

**Pro tip**: Link to other files rather than duplicating content

### 4. Automated Project Documentation
- `architecture.md` - System design, app structure, component interactions
- `changelog.md` - List of changes over time
- `project-status.md` - Milestones, accomplishments, where you left off
- Feature reference docs (optional) - High-level overview of key features

Ask Claude to update these automatically via CLAUDE.md instructions or slash commands.

### 5. Install Plugins
Recommended:
- Anthropic front-end plugin (better UIs)
- Anthropic feature dev plugin
- Every compound engineering plugin

### 6. Install MCP Servers
Based on your tech stack:
- Database MCPs (MongoDB, Supabase)
- Playwright/Puppeteer for web app testing
- Vercel for deployment
- Mixpanel for analytics
- Linear for project management

### 7. Custom Slash Commands and Sub-agents

**Slash Commands** = shortcuts to prompts (same context window)
**Sub-agents** = specialized agents (forked context, good for parallel work)

Recommended sub-agents:
- Changelog sub-agent
- Front-end testing sub-agent
- Retro agent (reflects and updates CLAUDE.md)

### Advanced Setup
- **Pre-configure permissions** - Auto-approve safe commands (git, file edits)
- **Hooks** - Scripts that run at lifecycle points (e.g., check tests pass, Slack notifications)

---

## Phase 3: BUILD

### Building Your MVP
- Use plan mode first
- Ask Claude to use parallel sub-agents where possible
- Work through milestones from your project spec

### Workflow 1: Single Feature Development
1. **Research** (optional) - Research reports, API lookups
2. **Plan** - Use plan mode, let Claude break down steps
3. **Implement** - Use plugins, MCPs, slash commands
4. **Test** - Automated testing with sub-agents

### Workflow 2: Issue-Based Development
- GitHub issues = source of truth for features/bugs
- Ask Claude to convert project spec into GitHub issues
- Enables parallel work on multiple issues
- Use slash commands to create issues from specs

### Workflow 3: Multi-Agent Development
- Run multiple Claude Code instances simultaneously
- Use **git worktrees** for isolated working copies on different branches
- Each session works independently, then merge results
- Most advanced workflow

---

## Productivity Tips

1. **Use the best models** - Opus for planning/complex tasks, Sonnet for implementation, Haiku for simple fixes
2. **Periodically update CLAUDE.md** - Keep it in sync with project evolution
3. **Regression prevention** - Use `#` to add instructions to CLAUDE.md when Claude makes mistakes
4. **Don't be afraid to throw away work** - Use checkpoints and rewind; code is cheap

---

## Recommended Tech Stack (from video)

| Component | Tool |
|-----------|------|
| Frontend Hosting | Vercel |
| Framework | Next.js |
| Styling | Tailwind |
| Components | Shadcn |
| Database | MongoDB or Supabase |
| Auth | Clerk |
| Payments | Stripe |
| Email | Resend |
| Backend Hosting | Digital Ocean |
| Object Storage | Cloudflare R2 |
| AI | Anthropic models |
| Image AI | Imagen from Google |

---

*Source: setup.md (video transcript)*
