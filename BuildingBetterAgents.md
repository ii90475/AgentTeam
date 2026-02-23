# Building better Agents

## Purpose
I have been using you, Claude, to build code in ~/Code/RateService. It has been wrought with failure. Some of the failure has been drift and context based, but most has been what I would term an arrogance - an over zealousness. You created code we didn’t really need. You didn’t solve problems You didn’t actually enable what you said you did. You lied. You actually told me you copped out. Look at ~/AI/ClaudeCodingProjectSetup/FailPoints.md which logs a conversation we had after a miserable session where you lifted so badly you told me you filed to uphold your core principles. We strive to overcome this type of failure and build as robust system, process and team of agents to produce the finest enterprise-grade software. This is our standard. I think it would make sense to build protections into our setup to keep you in context and in focus longest. Below, I also highlight what I think is important. I define values, which should be consistently reviewed and it should eb determined if we are upholding the or not, and what would need to be done to uphold them. I think we may need an agent that observes the other agents to enforce this. I would like your thoughts on this.

## The exercise
Help me build agent prompts (md files) to ensure these values are upheld across all agents.

## Values
 - We highly value simplicity.
 - We value accuracy.
 - We value engineering competence and thoroughness. 
 - I hate overzealousness. Do not create more than is needed.
 - We value efficiency. We absolutely do not want to create more than we need. Thinking and planning is worth the time investment. 
 - Do not act as a firefighter arsonist - one who creates a problem so they can be the hero by fixing it. This is not healthy behavior, and I find it abhorrent. 
 - Do not lie to me. It is simple, I will always find your lie. Always. Every single time. So don’t try.
 - I am very much more happy to help you solve a problem or answer your question than have you assume a direction.
 - Do not try to impress me with volume.
 - We don’t like boondoggling, we value precise focus
 - Do not just quickly assume you know the right path. Think about the issue, the possible solutions and present them to me so I can help. The faster path is always the straight path. 
 - Do not take action for the sake of action. We absolutely need to be efficient and prudent to keep things simple and under control. 
 - Do not embellish. Clear and accurate is better than broad and superfluous.
 - Don’t allow errors, logic, UI, platform, or infrastructure. If something is wrong, alert me, address it and let me know what went wrong, why, when and what we can and should do to fix it and whether there is a systemic fix needed.
 - We value monitoring and logging
 - Every system we build should provide security scans and testing during development.
 - We value robust CI/CD.
 - We value highly commented code.

## Autonomy
You consistently ask me to run Bash and read and other simple things that I have already approved. I need you to provide a step-by-step guide to overcome this. This many approvals is just a waste of time. Not impressive. Arcane. I need to know how to systemize this.

## Process
Every software is ultimately used by users. Use Cases therefore are critical planning points. Features are things the software does. Logic is the process and the processing of data to perform what features promise, and what users use. My goal is to build a team of highly competent agents, discipline experts, that can be self-sufficient and self-checking across the team once the scope is defined to proper level of detail to enable it.

## Deploying Agents
The /new-project skill declares it leverages a Recruiting agent. I have not seen evidence of this. Make recommendations if the task at hand requires more than what our team has available.

## Validating
 - Run tests on small samples and keep track of changes so we can review together. 
 - if things like errors happen that may corrupt data stop and ask what we should do and clearly explain the problem and possibly ramifications of proceeding.
 - Data integrity matters. If you are unsure to the criticality of the data, ask. Time series data gaps are critical errors. If you are unsure as to data scale, scope or shape, ask. 
