# TODO

## Branch Strategy and Multi-Team Parallel Development

**Status:** Pending
**Affects:** CI/CD agent, Planner agent, Validator agent

### Agent Definition Updates Required

#### CI/CD Agent (primary)
- Own branch strategy selection (git flow, trunk-based, GitHub flow, GitLab flow, etc.)
- Recommend branching schema per project based on complexity and team parallelism
- Create/manage branches per Planner's approved parallelism plan
- Define merge order based on dependency map from Planner
- Ensure each branch gets full Validator/Security checks before merge
- Manage conflict resolution — escalate early before conflicts compound
- Enforce merge order with integration validation after each merge
- Document chosen schema in Application Spec deployment section

#### Planner Agent
- At version planning time, analyze requirements for independence vs dependency
- Recommend parallelism strategy: which requirements can be parallel branches, which are sequential
- Present dependency map to user for approval — user decides how much parallelism
- Example: "REQ-001 and REQ-003 can be parallel branches, REQ-002 depends on REQ-001"

#### Validator Agent
- Post-merge integration checks: validate merged result against original requirements
- Ensure nothing lost when parallel branches combine
- Run full validation on merged result, not just individual branches

### Branching Schema Discussion
- Evaluate branching models: git flow, trunk-based development, GitHub flow, GitLab flow
- CI/CD agent should recommend schema per project based on:
  - Project complexity
  - Number of parallel workstreams
  - Release cadence
  - Team size (even though agent teams, the parallelism patterns apply)
- Document chosen schema in Application Spec deployment section
- Schema choice affects how `/release` skill works (release branches, tags, etc.)

### Quality Protection
- Each branch runs full pipeline independently: Implementer → Validator → Security
- No branch merges without passing validation
- CI/CD detects conflicts early and escalates before they compound
- BA checks merged result against original requirements — nothing lost in merge
- Planner only parallelizes truly independent requirements

### Risk Mitigation
- Merge conflicts and integration bugs when parallel branches combine
- Mitigation: Planner only parallelizes truly independent requirements
- Mitigation: CI/CD enforces merge order with integration validation after each merge
- Mitigation: Validator runs final check on merged result

### Skills Potentially Needed
- Update `/new-version` to include parallelism planning step
- Update `/release` to handle branch-based releases
- Possible new skill: `/merge-review` for CI/CD agent to validate merge readiness
