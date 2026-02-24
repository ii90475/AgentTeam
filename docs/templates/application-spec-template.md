# {Project Name} — Application Spec

**Created:** {YYYY-MM-DD}
**Status:** Active | Archived

---

## Overview
<!-- PO fills this in. What is this app, who is it for, why does it exist. -->

**What:** {one-sentence description}
**Who:** {target users}
**Why:** {problem it solves}

---

## Related Applications

| App | Relationship | Integration Point |
|-----|-------------|-------------------|
| {app} | Parent/Child/Sister/Dependency | {how they connect} |

---

## Architecture
<!-- Planner/Technology Analyst fills this in. Updated when infrastructure changes. -->

**Tech stack:**

| Layer | Technology | Rationale |
|-------|-----------|-----------|
| Frontend | {tech} | {why} |
| Backend | {tech} | {why} |
| Database | {tech} | {why} |
| Infrastructure | {tech} | {why} |

**System design:**
{high-level architecture description or diagram reference}

**Dependencies:**
- {external services, APIs, libraries}

---

## Security Model
<!-- Security agent fills this in. Updated when security posture changes. -->

**Auth model:** {authentication approach}
**Data sensitivity:** {what data is sensitive, how it's protected}
**Threat considerations:**
- {threat → mitigation}

---

## Deployment
<!-- CI/CD agent fills this in. -->

**Environments:**

| Environment | Purpose | URL/Location |
|-------------|---------|-------------|
| Dev | Development | {url} |
| Staging | Pre-production | {url} |
| Production | Live | {url} |

**Release process:**
1. {step}

---

*Maintained by: Planner, Security, CI/CD agents. Updated when application-level concerns change, not per version.*
