---
description: Trigger technology research for a specific topic
---

Conduct technology research using the Technology Analyst agent.

**Research topic**: $ARGUMENTS

Follow these steps:

1. If no topic was provided above, ask the user what they want to research

2. Determine project context:
   - Check if this research is for a specific project in docs/projects/
   - If unclear, ask user which project this is for (or if it's cross-project)

3. Use the Technology Analyst agent to:
   - Clarify requirements and constraints with the user
   - Research 3-5 viable options using web search
   - Create a comparison matrix with weighted scoring
   - Provide a clear recommendation with rationale
   - Save the report to the appropriate location:
     - Project-specific: docs/projects/{project}/research/{topic}-research.md
     - Cross-project: docs/decisions/

4. Present the recommendation summary to the user

5. If user approves the recommendation:
   - Update docs/decisions/technology-decisions.md
   - Update project architecture.md if applicable
