---
description: Initialize a new project with documentation structure
---

Initialize a new project using the Project Manager agent.

**Project name**: $ARGUMENTS

Follow these steps:

1. If no project name was provided above, ask the user for one
2. Use the Project Manager agent to:
   - Create the folder structure at docs/projects/{project-name}/
   - Create docs/projects/{project-name}/research/ subfolder
   - Copy and customize templates from docs/templates/
   - Gather project goals, milestones, and initial tasks from the user
   - Initialize all documentation files

3. Ask the user if they want to define the tech stack now
4. If yes, use the Technology Analyst agent to:
   - Research appropriate technologies based on project requirements
   - Document initial stack choices in architecture.md
   - Record decisions in docs/decisions/technology-decisions.md

5. Confirm the project is ready for development
