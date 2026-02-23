# Overall Plan: Maximizing Agent Team Across All Workloads

**Version:** 1.0.0
**Date:** 2026-02-22
**Optimization Priority:** Security > Time (done right first) > Token efficiency

---

## Prime Directive

**Security is the single most important value. It overrides all other values, goals, and pressures.**

Every recommendation in this plan is evaluated against this directive first.

---

## 1. Current State Summary

### What You Have

**Production Systems (Tier 1):**
- **RateService** (v0.37.5) - Real-time FX rates, TimescaleDB, 95%+ test coverage
- **TradingSystem** (v0.42.2) - Trading dashboard, 961 tests, 93% coverage

**Active Development (Tier 2):**
- **PersonalAssistant** - Obsidian vault, 1,698 notes, Phase 1b migration
- **ClaudeCodingProjectSetup** - Agent team framework (this project)

**Planning/Future (Tier 3):**
- Financial planning guides (TaxAndRetirementAdvisor, RetireEarly)
- Personal development (LifeCoach, SystemsOverGoals)
- Business systems (BankingSystem, TsionasPay, UDPay)

**Legacy (Tier 4 - Inactive):**
- 10+ trading bots (Tradernaught, EasyBot, SimpleBots, etc.)
- Data readers (ReadOanda, ReadCitadel)

**Content/Blogs (Tier 5):**
- YTCCSBE (YouTube)
- TradingGuidance
- WSJ-related project

### What You Want

- Scores of applications to build
- Half dozen blog and YouTube sites
- Several businesses
- Automated trading (already in progress)
- All done right the first time
- Security paramount

---

## 2. Organizational Structure

### Directory Architecture

```
~/
├── AI/                                    # AI/Claude workspace
│   ├── CLAUDE.md                          # Global Prime Directive + Framework
│   ├── ClaudeCodingProjectSetup/          # Agent Team definitions (this project)
│   │   ├── agents/definitions/            # Agent team (source of truth)
│   │   └── templates/projects/            # Project templates
│   └── [learning projects]/               # Claude learning, certifications
│
├── Code/                                  # Active development
│   ├── _archive/                          # Legacy projects (create this)
│   ├── trading/                           # Trading ecosystem (reorganize)
│   │   ├── RateService/
│   │   ├── TradingSystem/
│   │   └── shared/                        # Shared libs if needed
│   ├── business/                          # Business applications
│   │   ├── TsionasPay/
│   │   ├── UDPay/
│   │   └── [new businesses]/
│   ├── content/                           # Blogs, YouTube, content
│   │   ├── YTCCSBE/
│   │   └── [blog sites]/
│   └── personal/                          # Personal tools
│       ├── PersonalAssistant/             # Or keep in ~/AI
│       └── HomeLab/
│
└── .claude/                               # Global Claude config (if supported)
```

### Every Project Gets

1. **CLAUDE.md** - With Prime Directive at top, project-specific instructions below
2. **Agent team reference** - Points to ~/AI/ClaudeCodingProjectSetup/agents/
3. **State directory** - For Context Keeper to maintain across sessions
4. **Requirements.md** - For Business Analyst to own
5. **Security baseline** - Defined security requirements per project type

---

## 3. Agent Team Deployment Strategy

### Global Configuration

Add to `~/AI/CLAUDE.md` (already done):
- Prime Directive
- Reference to agent definitions
- Session start protocol

### Per-Project Configuration

Each project's CLAUDE.md should contain:

```markdown
## Prime Directive
[Copy from global - security override]

## Agent Team
This project uses the agent team defined in:
`~/AI/ClaudeCodingProjectSetup/agents/`

At session start:
1. Context Keeper reads state/session-log.md
2. Context Keeper provides performance report
3. BA confirms requirements are current
4. Work proceeds per agent workflow

## Project-Specific Instructions
[Project details here]
```

### Session Protocol

**Every session, regardless of project:**

1. **Context Keeper** reads state, provides report
2. **Context Keeper** checks for agent violations in previous session
3. **BA** confirms requirements are still valid
4. User confirms focus
5. Work proceeds through Planner → Implementer → Validator

**This prevents drift, maintains context, catches issues early.**

---

## 4. Project Prioritization

### Immediate (This Week)

| Priority | Project | Action | Agent Focus |
|----------|---------|--------|-------------|
| 1 | **ClaudeCodingProjectSetup** | Complete agent definitions, test on real project | All agents |
| 2 | **RateService** | Add CLAUDE.md with agent team, create state/ dir | Context Keeper, Validator |
| 3 | **TradingSystem** | Update CLAUDE.md with agent team, create state/ dir | Context Keeper, Validator |

### Short-term (This Month)

| Priority | Project | Action | Agent Focus |
|----------|---------|--------|-------------|
| 4 | **PersonalAssistant** | Complete Phase 1b migration, add agent team | BA, Context Keeper |
| 5 | **Archive legacy** | Move inactive bots to ~/Code/_archive | Context Keeper |
| 6 | **Template validation** | Test project templates with agent team | All agents |

### Medium-term (Next Quarter)

| Priority | Project | Action | Agent Focus |
|----------|---------|--------|-------------|
| 7 | **New business apps** | Scaffold using templates + agent team | Full workflow |
| 8 | **Content/blogs** | Create content project template, scaffold sites | BA, Planner |
| 9 | **Integration testing** | RateService ↔ TradingSystem | Validator, Security |

---

## 5. Security Integration

### Per-Project Security Baseline

Every project must have defined:

```markdown
## Security Requirements

### Data Classification
- [ ] What sensitive data does this project handle?
- [ ] PII? Financial data? Credentials?

### Authentication
- [ ] How are users authenticated?
- [ ] How are services authenticated?

### Secrets Management
- [ ] Where are secrets stored?
- [ ] Are they in .env files? (Must be in .gitignore)
- [ ] Are they in environment variables?

### Dependencies
- [ ] Dependency audit scheduled?
- [ ] Automated vulnerability scanning?

### Access Control
- [ ] Who can access production?
- [ ] How is access logged?
```

### Security Subagent Checkpoints

Security subagent runs at:
1. Before any commit (pre-commit hooks)
2. Before any deployment
3. Weekly scheduled audit
4. Any time credentials/secrets are mentioned

### Trading System Security (Critical)

**RateService and TradingSystem handle real money. Extra requirements:**

- API keys must never appear in logs
- All database connections must be encrypted
- Rate limiting on all endpoints
- Audit logging for all trades
- Circuit breakers tested and documented
- Rollback procedures documented and tested

---

## 6. Time Optimization Strategy

### "Done Right First Time" Principles

1. **Plan before code** - Planner agent presents options, gets approval
2. **Requirements before planning** - BA documents before Planner plans
3. **Small iterations** - Validate frequently, catch issues early
4. **No scope creep** - BA guards boundaries, Validator checks
5. **Test as you go** - Validator runs tests at each checkpoint

### Anti-Patterns to Eliminate

| Anti-Pattern | Agent That Prevents It |
|--------------|------------------------|
| Starting without requirements | BA blocks until documented |
| Coding without plan approval | Planner requires explicit approval |
| Adding unrequested features | Validator checks scope |
| Claiming untested functionality | Validator verifies claims |
| Drifting from original intent | Context Keeper tracks decisions |
| Repeating past mistakes | Context Keeper reads FailPoints.md |

### Parallel Work Strategy

When working on multiple projects:

1. **Clear session boundaries** - One project per session when possible
2. **State files** - Context Keeper maintains state per project
3. **Cross-project awareness** - Note dependencies in requirements
4. **Weekly review** - Context Keeper triggers periodic review

---

## 7. Content/Blog Strategy

### Content Project Template

Create new template: `templates/projects/content-site.md`

```markdown
# Content Site Template

## Structure
- content/           # Posts, articles, scripts
- assets/            # Images, videos, graphics
- site/              # Static site generator config
- analytics/         # Tracking, metrics

## Workflow
1. BA: Define content calendar, audience, goals
2. Planner: Outline content pieces
3. Implementer: Write/create content
4. Validator: Fact-check, SEO review, accessibility

## Security
- No credentials in content
- Image alt text (accessibility)
- HTTPS only
- Comment moderation if enabled
```

### For YouTube Specifically

- Script review by BA (does it match channel goals?)
- Technical accuracy by Validator
- SEO/discoverability check
- Thumbnail accessibility review

---

## 8. Business Application Strategy

### Business App Security Requirements (Elevated)

All business applications handling money or customer data:

1. **Security subagent runs on every change** - Not just weekly
2. **Penetration testing** - Before any production deployment
3. **Compliance check** - PCI-DSS if payments, GDPR if EU users
4. **Incident response plan** - Documented before launch
5. **Backup/recovery tested** - Before launch

### Business App Template

Extend `templates/projects/api-service.md` with:

- Compliance requirements section
- Data retention policy
- Audit logging requirements
- Customer data handling procedures

---

## 9. Automated Trading Strategy

### Current State

- RateService + TradingSystem are production-ready
- 93%+ test coverage
- Monitoring with Prometheus/Grafana

### Agent Team Integration

For trading systems specifically:

1. **BA** - Define trading strategy requirements precisely
2. **Planner** - Present backtesting plan before live
3. **Implementer** - Code with extensive logging
4. **Validator** - Must verify:
   - Backtesting results match expectations
   - Risk limits enforced
   - Circuit breakers functional
   - No regressions in existing strategies
5. **Security** - API key handling, no credentials in logs
6. **CI/CD** - Deployment must not interrupt live trading

### Trading-Specific FailPoints

Add to FailPoints.md tracking:
- Data integrity issues (gaps, incorrect rates)
- Order execution failures
- Risk limit breaches
- Strategy drift from specification

---

## 10. Implementation Roadmap

### Phase 1: Foundation (Week 1)

- [ ] Archive legacy projects to ~/Code/_archive
- [ ] Add CLAUDE.md with agent team to RateService
- [ ] Add CLAUDE.md with agent team to TradingSystem
- [ ] Create state/ directories for Context Keeper
- [ ] Test full agent workflow on one small task

### Phase 2: Production Hardening (Week 2-3)

- [ ] Security audit of RateService with Security subagent
- [ ] Security audit of TradingSystem with Security subagent
- [ ] Document all secrets locations
- [ ] Verify all .gitignore files exclude sensitive data
- [ ] Test CI/CD subagent on deployments

### Phase 3: Expansion (Week 4+)

- [ ] Complete PersonalAssistant Phase 1b
- [ ] Create content-site template
- [ ] Scaffold first new blog/YouTube project with agent team
- [ ] Scaffold first new business app with agent team

### Phase 4: Optimization (Ongoing)

- [ ] Weekly reviews per Context Keeper schedule
- [ ] FailPoints.md → agent definition updates
- [ ] Refine templates based on usage
- [ ] Document lessons learned

---

## 11. Success Metrics

### Security

- Zero credential exposures
- Zero security incidents
- All projects pass Security subagent audit
- All dependencies audited monthly

### Time

- Requirements documented before planning (100%)
- Plan approved before implementation (100%)
- Scope creep incidents (target: 0)
- Rework due to unclear requirements (target: 0)

### Quality

- Test coverage maintained (>90% for critical systems)
- Validator catches issues before user (target: 95%)
- Context maintained across sessions (no "where were we?")

---

## 12. Risk Mitigation

### If Agent Team Adds Overhead

The agent workflow (BA → Planner → Implementer → Validator) may feel slow initially. Mitigation:

1. Skip for trivial tasks (<5 min estimated)
2. Combine phases for well-understood work
3. Trust builds over time as agents prove value

### If Context Gets Lost Anyway

If Context Keeper fails to maintain state:

1. Increase state file detail
2. Add more checkpoint summaries
3. Consider external memory tools (Obsidian integration?)

### If Security Slows Development

Security checks take time. But:

1. Catching issues early is faster than fixing breaches
2. Security subagent should optimize over time
3. Pre-commit hooks catch obvious issues fast

---

## 13. Next Steps

**Immediate actions for you:**

1. Review this plan
2. Approve or modify priorities
3. Decide on directory reorganization (~/Code/trading/, etc.)

**Immediate actions for me:**

1. Wait for your approval
2. Begin Phase 1 implementation
3. Create first project CLAUDE.md with full agent team

---

## Appendix: Quick Reference

### Session Start Checklist

```
[ ] Context Keeper: Read previous state
[ ] Context Keeper: Check FailPoints.md
[ ] Context Keeper: Performance report
[ ] BA: Confirm requirements current
[ ] User: Confirm focus for session
```

### Before Any Code

```
[ ] Requirements documented (BA)
[ ] Plan presented and approved (Planner)
[ ] Security implications considered
[ ] Test approach defined
```

### Before Any Commit

```
[ ] Tests pass (Validator)
[ ] Security scan clean (Security subagent)
[ ] Scope verified (Validator)
[ ] Claims verified (Validator)
```

### Before Any Deployment

```
[ ] CI/CD checks pass (CI/CD subagent)
[ ] Security audit current (Security subagent)
[ ] Rollback tested
[ ] Monitoring confirmed
```
