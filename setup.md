Don't make the same mistake I did
I used to start my Claude Code projects completely wrong. I typed Claude into my terminal and just start freestyle prompting
with no planning, no setup, and no system for building. It was like trying to build a house without blueprints.
I eventually got something built, but it was messy, inefficient, and full of problems. I could have avoided.
But after building dozens of projects with Claude Code over the past year, I've discovered a simple three part system that makes every project
10 x easier to build from day one. And in this video, I'm gonna save you months of frustration and wasted time
by sharing the exact system that I use to start every new Claude Code project. I call it the PSB system for plan, setup, and build.
Phase one is plan. This is where you set up your project for success. Before you write a single line of code.
We'll cover the two critical questions I asked myself before building and creating a project spec doc that combines both product
requirements and engineering design. So Claude can build exactly what you want the way that you want it.
Phase two is set up. This is where you configure Claude code with everything that it needs to build effectively.
We will cover my seven step set up checklist for Claude Code from setting up a GitHub repo and creating your claude.md file to advanced features
like plugins, MCPs, and custom commands. Phase three is build.
This is where you'll start writing code first by building your MVP and then the rest of your project milestones.
We'll cover the three development workflows that I use for every project, the general workflow for single features, issue-based
development for staying organized and multi-agent development, for working on multiple features simultaneously.
Plus, I'll share the most important tips that I've learned to keep your building process with thought code productive and efficient.
So whether you're starting your first Claude Code project, or you already use Claude Code every day, I guarantee that you're gonna learn something from
this video that's gonna help you build faster, that smarter with Claude Code, even if you don't use a whole system.
And just apply a handful of these tips that I'm gonna share. But before we dive in, I'm Avthar and I teach people about the best AI coding
tools and how to get the most out of them, no matter your skill or experience level. So if trying to level up with AI coding tools, maybe it's for your job
or for your business, or maybe even a side project, please subscribe to the channel and turn on notifications for more videos about AI coding.
Alright, with that out the way, let's get into phase one of starting a new Claude Code project.
And that's planning. We're gonna cover the two most important questions to ask yourself. How to create a project spec doc that captures both product and engineering
Phase 1: PLAN
requirements and how to use AI to help you plan at every step of the way. And look, I get it.
Planning sounds boring. You wanna start coding. But trust me on this one, spending just 15 minutes, planning a project
upfront will save you hours, sometimes even days of frustration down the line. Now before I even open Claude Code, I do a brainstorm of what
2 Questions to ask before starting
I want to achieve with a project. Specifically. I ask myself two questions and note down the answers using a
pen and paper or a Google Doc. The first question that I asked myself before building is, what
are you actually trying to do? Or what is the goal of your project? Are you trying to learn a new technology?
Are you trying to validate an idea with customers? Are you building an alpha version of a product or feature, or
are you just prototyping to see if something is possible? Getting clear about what you're actually trying to do changes everything
about how you approach the project. It tells you what's important to build versus what you can skip.
For example, if you're just trying to prototype to see if a feature is a good idea, you can just focus on the core functionality for that feature.
You don't need to worry about production ready code or edge cases. You can move fast and break things, but if you're building something you wanna
ship to real users, then you need to think about things like security, error, handling, edge cases, and all the details that make your product feel polished.
A key thing to keep in mind when you're planning is that the clearer you are, the better. Claude will understand what you're trying to achieve and build accordingly.
The second question I ask myself in the plan phase is, what are the milestones of functionality that you want?
This is where you can start breaking down your project into clear phases. What does version one look like?
Maybe it just focuses on one core feature. What are you okay with leaving out or saving for future versions?
then you can apply that same thinking to version two, version three, and so on.
For most projects, I like to think in terms of an MVP or minimum viable product, and then one or two versions of improvements.
The MVP is an absolute minimum. You need to validate your idea or prove that the concept works.
And then in future versions you can add things like scaffolding, polish or optimizations.
How to use AI to help you plan
Next up in phase one is using AI to help you plan. Once you have your brainstorm, this is where you can use AI to help you
flesh out the plan for your project. And here's my pro tip for using any AI to help you plan,
tell it to ask you questions. For example, when I start a new project, I give Claude my brainstorm in a
markdown file and ask, "Hey Claude, I wanna build this project. What are the three most important questions I need to answer in order to build an
MVP of this successfully?" Claude will then ask me clarifying questions about the brainstorm to help me spot things that I haven't fully thought through,
or decisions that need to be made. And by answering these questions, I get way more clarity about what
I'm actually trying to build. The cool thing is that you can repeat this trick of getting the AI to ask you questions for any aspect of the planning or building process,
whether it's figuring out product requirements or technical tool choices, or just debugging an gnarly issue.
The other tool that I use for planning is just having a conversation with a Claude assistant or ChatGPT, using voice mode . I literally just talk through
my project idea out loud, talking about the different features that I want the user flows, and then I ask it to summarize our conversation and put
it in a markdown file that I can use as a starting point with Claude Code. Having a voice conversation with AI is super useful in the planning
process ' cause that's when your ideas are still fuzzy and sometimes it's hard to write things down because you don't even know what you think.
And so saying it out loud helps you process your ideas a lot more easily. Alright, so now we get to the main deliverable of the planning phase,
Creating a project spec doc
which is your project spec doc. The project spec has two main parts, the product requirements
and the engineering requirements. It contains the essential product ideas and engineering design
information to help Claude Code successfully build your project. I'll note that how detailed your project spec doc needs to be depends on your
project goal and your milestones. This is why it's important to get clear on those first. Now if you worked at a software company before, you might be familiar with a
product requirements DOC or PRD and Engineering Design Docs, or EDDs, the
project Spec Doc is basically a much more lightweight version of that, but tailored for building with Claude Code.
Let's dive into the first part of your project Spec doc, which is the product requirements. The product requirements are about what you're building and why.
It answers three key questions. Who is a product for? What problems does it solve, and what should the product do?
This is where you exercise your creativity, your insight, and your product sense. You need to think about who you're building for and what
problems you wanna solve for them. Sometimes that person is you, so take some time to think about it.
And here's what I've learned about product requirements. You'll likely need to spend some time outlining exactly what you
want in terms of how the problems are solved from a user perspective. ' cause if you're not specific about the user interactions that you want,
Claude might make assumptions and you might not like what you get. For example, if you're building a journaling app, don't just say
users can create journal entries. Be specific. What does creating an entry look like?
Do they start with a blank page or do they start with prompts? Can they add photos? Can they edit past entries?
What does a workflow look like? The more specific you are about the user experience that you want, the
better Claude will be at building it. Another key thing to keep in mind for the product requirements is don't
try to build everything at once. Break your project down into clear milestones for capabilities.
This is where the milestone question we asked ourselves earlier comes in handy. What are the most important things to build first and define what done
looks like for each milestone so you have a clear target to hit. The final pro tip around product requirements is that if you're
not sure about your product requirements, that's totally okay. Build version one first, and then based on what you like or dislike about it, you
can create a plan for version two, iterate on your product requirements as you build. Alright.
All right. The second part of your project spec is the technical requirements or engineering design doc.
While the product requirements cover what you're building, the engineering design is about how you're building it.
The first and most important part of your engineering requirements is choosing your tech stack.
Now, depending on the type of product that you're building, you'll need to decide on things like what programming language you're going to use, your
preferred front-end framework. Backend framework, things like your database choice, your hosting and
info provider, as well as any other details about the components that you'd like to use in your project.
And here's why that matters for Claude Code. If you don't specify your stack, Claude might just inject random technology
choices that you might not want. So I always start by being rarely explicit about my stack preferences.
If you are looking for inspiration, here's my preferred stack for building web applications. For the front end, I use Vercel for Hosting Next JS as a framework, tailwind
for styling and Shadcn for components. For the backend and database, I like MongoDB or Supabase
depending on the project. For authentication and login, I use Clerk. And for payments, you can't go wrong with Stripe.
For email, I've been enjoying Resend recently and for backend hosting if I need it I use Digital Ocean . For object storage.
My go-to is Cloudflare R2. And for AI features I tend to use Anthropic models, but for images I
use nano banana from Google Gemini. Now if you prefer different technologies, that's totally fine.
You don't have to use this stack. It's just a suggestion. But the main thing is that you should be clear about what you want Claude to use.
But what if you're not sure about what to use or even what components of the stack you need in the first place?
The answer here is just ask Claude . Describe your requirements and ask Claude code to create a research report with options and recommended choices for you.
Claude Code has web search built in so it can look up the latest docs, tools, and frameworks and give you informed recommendations.
The second part of your technical requirements is defining your technical architecture. This includes things like your system design, overview, the key components of
your app and how they interact, as well as your database schema, your API design, if you have one, and other technical details that matter for your project.
Now I usually delegate most of this to Claude, but if you're using Claude Code at work or on a team, you likely wanna be more prescriptive with the
implementation details in order to follow the best practices that your team uses. For example, if you're working at a company that has specific patterns
for system design, you might wanna document those in your engineering design so that Claude follows them.
And part of this technical architecture step often involves actually provisioning the infrastructure that you need.
So once you've decided what infra you want to use, go ahead and provision it. Create your database.
Set up your hosting, create your API keys. Do it all now so that Claude can move fast when you start building.
So that wraps up the planning phase. you're now ready to move to phase two, which is Claude Code setup.
Phase 2: SETUP
Alright. Phase two is a setup phase. This is where we're gonna cover the seven step checklist that I use to set up
Claude Code for successful development. And by the end of this section, your Claude Code is gonna feel like a perfectly
tuned instrument with all the shortcuts, automations, and context that it needs to build your project effectively.
Heads up that you don't need to use all the things I recommend in the setup section to improve your existing workflow.
Just pick and choose the things that you feel is relevant to your project. Step one in the setup checklist is set up a GitHub repo for your project.
GitHub Repo setup
Now you can just build locally with Git, but I strongly recommend setting up a GitHub repo from the start for a few key reasons.
First setting up a GitHub repo enables you to use Claude Code on the web and mobile so you can code from anywhere.
Second, you get access to the GitHub CLI and the Claude Code gitHub Action. This is super useful for reading project and branch history
and creating pull requests. And the GitHub action is useful for automated PR reviews and
mentioning Claude to handle issues. Third. Many infrastructure providers like Vercel enable you to deploy just by
connecting a GitHub repo and in the case of Vercel It also supports deploy previews for each branch of your project.
This makes using branches a no brainer for developing new features or trying new product directions while keeping your main branch stable.
Generally, I ask Claude Code to use a new branch for each big new feature that it develops, and then when it's done, we merge or submit
a PR against the main branch. Fourth and finally, a GitHub repo enables issue-based development.
This helps keep your project super organized as it makes GitHub issues the source of truth for things like bugs and feature requests.
And it also means that you can use multiple instances of Claude Code to tackle multiple issues at the same time.
We'll cover issue-based development and multi-agent development in more depth in the build section later in the video.
Create your environment variable file (.env)
Step two in the setup checklist is creating your environment variable file. To do this first, ask Claude to create an example ENV file based on
your project spec and tech stack. Then create a copy of that and fill in your needed credentials and API
keys so that Claude can build with them without stopping to ask you. Step three is setting up your claude.md file.
CLAUDE.md (and what to put in it)
You can think of your Claude.md file as your project's memory. It's always included in context for every chat that you have with Claude Code.
A big thing to remember about your Claudemd file is that it is finite so don't bloat it.
You wanna keep it focused on the most important information. So what goes inside a Claudemd file?
Now, there's no one size fits all answer, but in general, you wanna put information about your project that Claude absolutely needs to know.
Here are some suggestions about what to include. First, the project goals and a project architecture overview.
This gives Claude a big picture, grounding of the project and the folder layout. Next is a design style guide and user experience guidelines.
This keeps your code that is generated by Claude, aligned with your project and design goals.
Then constraints and policies. This prevents unsafe or forbidden actions. For example, you can tell Claude never to push to the main branch directly or always
use environment variables for secrets. Then repository etiquette. For example, telling Claude when to use things like PRs versus direct merges, how
to name branches and other git workflows. You can also put frequently used commands like those for building and testing so
that Claude can run them without asking. And you can also include testing instructions and other rules and
constraints that you want Claude to follow in your Claude.md file. One of the most impactful ways that I've found to keep your Claude.md
Concise is to link off to other files. Tell Claude about files that have important context in the
Claude.md file and tell it to reference them for the full picture. For example, you can link off to your project spec doc from the plan phase,
as well as an Architecture MD file versus repeating that information. That way you can give Claude important information about your
project without unnecessarily clogging up the context window. Now finally, don't worry about making your Claude.md file perfect on day one.
You'll build it up iteratively as you work on your project, and we'll cover more about this in the build phase later in the video.
Automated Project Documentation
Step four in the checklist is to set up automated documentation. Automated documentation is my term for a set of documents that is separate
from your Claude.md file that maintains context about your project, which Claude can read when it needs to.
These are the sort of docs that you link off to in your Claude MD . You ask Claude to keep these docs up to date as you work.
That way you always have the latest context in your sessions. This is incredibly useful for development planning or even just refreshing your
memory about a project or feature. I have four core documents that I set up for every project.
Doc. Number one is the architecture.md file. Architecture.md documents your system design, app structure, and
how the major components interact. You wanna keep this updated after you add big features.
Document number two is a change log md. A change log is just a list of things
that's change in your project over time. It's common for companies to put out change logs whenever they do new releases or at the end of every week or every month.
This is helpful for Claude Code projects because it helps you see what work has been done, and also gives Claude an overview of how
the project has evolved over time. Doc number three is a project status doc.
This doc covers three things. What are the project milestones? What have you already accomplished in relation to those milestones and
where did you end off last time? The project status file is a personal favorite of mine 'cause I tend to work in
bursts and sometimes don't touch a project for a few days or even a few weeks. And so it's helpful for me and Claude to pick back up right where we left off.
Doc number four is reference docs for key features. These are technically optional since you can just use the code
base search subagent in Claude Code. But I like building these to get a high level overview of a feature so that I can
plan how to improve it or fix bugs in it. For example, in an iOS app that I was building, I had reference docs for
onboarding and push notifications. And in a web app that I was building, I had docs about how payments were
implemented, about how time zones worked in an email reminder feature and other docs documenting rules around core product functionalities.
Finally, how do you keep these docs updated? The answer is to ask Claude to automatically update the docs as it
works either with an instruction in your Claude.md, or using a custom slash command that Claude can run after it finishes a feature.
This is my personal preference for how to do automated documentation. Step number five in the setup checklist is to set up plugins for your project.
Install Plugins
Plugins extend Claude Code with specialized commands and workflows that make development faster and easier.
A plugin consists of any combination of slash commands, sub-agents, MCP servers, hooks, and skills.
Plugins enable you to easily take the best customizations from other Claude Code users and use them in your own projects without recreating them.
You can find plugins using one of the many plugin marketplaces around and you can manage them using the slash plugins command in Claude Code.
And if you're looking for inspiration, here's some plugins that I recommend using for new projects.
First up is the Anthropic front-end plugin. This adds specialized skills for front-end development, giving you better UIs and
avoiding that dreaded purple gradient. Second is the anthropic feature dev plugin, which helps streamline
the feature development process. And thirdly is the every compound engineering plugin.
This adds a whole suite of useful slash commands and subagents with the goal of making every feature easier to develop than the last, helping
your project continuously improve. Step six in the setup checklist is setting up MCPs or model context protocol servers.
Install MCP Servers
MCPs are integrations that connect Claude Code to external tools and services. They're incredibly useful because they let Claude interact with your
database, test your front end, deploy to hosting and do all sorts of other things that it couldn't do otherwise.
So which MCPs should you set up for a new project? This is where your tech stack from the plan phase comes in handy.
You might not need all of them, but try out the MCPs for key parts of your tech stack that you think would speed up your work.
For database work, I usually set up the MCP for whichever database I'm using. For example, the MongoDB, MCP or the Supabase, MCP.
This is especially important when you're rapidly iterating and adding features 'cause Claude can just update your database schema automatically.
For web apps, I recommend using the playwright MCP or the puppeteer MCP. These help Claude Code see your web app in action, which is super useful for things
like automatically testing user flows. Other MCPs from my recommended tech stack include the Vercel MCP for deployment,
the Mixpanel MCP for analytics and the linear MCP for project management.
To connect MCPs, just follow the commands in the docs for the MCP server of your choice, there's usually a one line install to add it to Claude Code.
Setup Custom Slash Commands and Sub-agents
Step seven, and the final step in the setup checklist is setting up slash commands and subagents.
Now, both slash commands and subagents are automated ways for Claude to perform specific tasks and workflows, but they work differently and understanding
the difference is really important. A slash command is a shortcut to a prompt or a task.
It uses the same context window as your main conversation. In contrast, a subagent is a specialized agent for a specific task.
It uses a fork of your context window, which means that it's unrelated to your main conversation and other subagents.
Now, this means that subagents don't know about each other this makes them perfect for parallel work and specialized tasks that need focused context.
You can use the built-in slash commands and subagents that come with Claude Code. You can use third party ones from plugins, or you can even
create your own custom ones. Let's double click into subagents. For subagents, I like to use the built-in subagents for planning and
code base search in Claude Code. They work great out of the box and you can invoke them manually or let Claude
use them automatically when it sees fit. You can also create custom subagent, and if you're looking for ideas, here are
three that I recommend for new projects. First up is a change log subagent to create and update change log entries
After we've finished a feature. Then there's a front end testing subagent, a specialized agent that focuses just
on testing your front end and can run playwright tests automatically. And third is a retro agent that reflects on what can be improved
after a development session. And then it updates things like your Claude.md, your prompts, your
slash commands with its learnings. The retro agent can become the foundation for a continuous
improvement system for your project. Now for slash commands, from the anthropic plugin, there are some great
ones like the slash commit and slash PR commit for committing changes. I like to use the feature dev slash command all the time.
And of course, you can also create your own custom slash commands. For example, I have a slash command that updates all my project docs from the
automatic documentation in step five of the checklist based on recent changes. And then I have another one that creates GitHub issues based on an input
project spec or a prompt that I give it. Now I'm sure you can see how custom slash commands and subagents close the loop on
some of the other setup steps like the automated documentation and plugins and MCPs from earlier in the setup Checklist.
Advanced setup: Preconfigure Permissions
So that's the seven step setup checklist. But before we move on to phase three, I wanna share two bonus advanced setup
tips that'll save you a ton of time. These are not strictly required, but I find them useful for
advanced Claude Code users. Bonus step number one is to pre-configure permissions and settings.
This allows you to pre-approve or pre block certain commands so that Claude Code doesn't have to ask you, or you don't have to prevent Claude from running them.
For example, if you want Claude Code to always be allowed to run git commands or edit files without asking you, you can specify that in your settings.
Pre configuring your permissions helps avoid the frustrating problem of thinking. Claude is working on something, going to get a cup of coffee and then coming back
to find that Claude was actually stuck waiting for permission the entire time. Bonus step number two is to set up hooks for advanced automation.
Advanced setup: Hooks
Hooks, let you insert determinism into your Claude Code workflow. There are basically scripts that can run automatically at certain points in the
Claude Code lifecycle, like before a tool call or after Claude finishes a task.
For example, I use a stop hook that checks if test pass when Claude finishes and if they don't, the hook tells Claude to keep going and to fix them.
Another example of a hook that I use is a notification hook that pings me on Slack when Claude needs permission to do something so I don't have
to be at my terminal all the time. Hooks are pretty advanced and they can seem intimidating, but I highly recommend
you try them out and think about even just one hook that you can use in your workflow after watching this video.
Phase 3: BUILD
This brings us to the end of the setup phase. At this point, Claude has everything it needs to start building your project.
Next up is the final phase of the PSB process, the part that you've all been waiting for.
The build phase where we can finally start writing code with Claude. Alright. Phase three is the build phase.
This is where we'll start building our new project with Claude. And just as with the plan and the setup phases, having the right workflows in
the build phase makes all the difference between frustration and smooth sailing. So in this section, we're not only gonna cover building your MVP with
Claude, but we'll also cover three workflows that I recommend in general for building new features with Claude Code, plus the most important tips
that I've learned to keep your building process productive and efficient. Let's get into it.
Building Your MVP with Claude
First up is asking Claude to build your MVP. At this point you have your project Spec Doc and your milestones
for your project documented. The next step is to have Claude Build Milestone one of your
project based on your project spec. A pro tip here is to ask Claude to use parallel subagents where
possible during the implementation. This can speed up the development process significantly because
Claude can work on multiple parts of your project at the same time. And as always, I recommend using plan mode first so that Claude can
translate your project spec into its own implementation plan for better results. Now that you've built your MVP, let's talk about how to build the rest
of the milestones in your project. I am gonna share the three workflows that I use the most when developing with Claude Code.
They are the general workflow, the issue-based workflow, and the multi-agent workflow.
Workflow 1: Single Feature Development
First up is a general workflow. This is what I recommend using when developing a single feature end to end.
The general workflow has four parts, research, plan, implement. And lastly, test.
Research can involve asking Claude to create a research report or even using external research you've done in ChatGPT deep research.
Now the research step is optional, but I found it helpful for bigger features where Claude needs to make tech stack decisions or look up specific APIs
that I'm using for the first time. The plan step in the general workflow is perhaps the most important part.
In fact, the most common mistake I see people make with Claude Code is not using plan mode enough.
When Claude is in plan mode, it'll think through the task, break it down into steps, and ask you clarifying questions before it starts building.
This leads to way better results. And during implementation and testing claude will automatically use all the
plugins, sub-agents, MCPs and slash commands that we set up in phase two to help with implementation.
One example that I like to use explicitly is the feature dev slash command from the anthropic plugin.
You're probably realizing that this is where all the configuration that we did in the setup phase comes in handy as it helps us speed up development.
Workflow 2: Issue based development
Next up is workflow two, which is issue-based development. In this workflow, GitHub issues become your source of
truth for features and tasks. Rather than only prompting Claude directly, you can create GitHub issues
describing bugs, improvements, and new features, and ask Claude to work on them. This is part of the reason why we set up a GitHub repo for our project
in the setup phase of this video. It helps keep the project tidy because GitHub is your source of truth versus
having several to-do files or feature MD docs lying around in your repo. For issue-based development, you need to be disciplined about splitting
your work into GitHub issues. Now the good news is that you can ask Claude code to help take your
project spec and your milestones and turn them into GitHub issues. And of course, you can also create issues manually on the fly.
If you like the issue-based workflow, you can also automate it with a slash command or sub-agent. For example, I have a slash command that takes in a file or folder and
outputs a list of GitHub issues in my repo using the GitHub CLI. Another benefit of the issue-based development workflow is that it makes
it easier to do work in parallel. We will cover multi-agent workflows in just a moment in workflow three.
But conceptually, using GitHub issues means you can ask Claude to tackle multiple issues using sub-agents in the same session.
This is useful for fixing a bunch of bugs quickly in parallel. You can also use multiple instances of Claude Code to tackle issues in
parallel, this is useful for adding multiple bigger features at the same time.
Workflow 3: Multi-Agent Development (Multi-Clauding)
Workflow three is about multi-agent development. It's the most advanced development workflow and it enables you to work
on multiple features at the same time. The multi-agent workflow is also known as multi-clauding in Claude Code
because you run multiple Claude Code instances at the same time with each session working on a different feature.
Now you might be wondering, how do they stay coordinated? Won't the changes conflict with each other?
This is where git work trees come in. Git work trees let you have multiple working copies of your repo in different
directories each on a different branch. Git work trees means that each Claude Code session can work in its own
work tree with isolated files while still sharing the same git history. And when your multiple instances are done working, you can ask Claude
to merge the work trees together. Either directly into the main or into a feature branch so that
you can test and review further. This is what I usually do. I've used the multi-agent workflow to work on three features at once,
and it's incredibly powerful. But it does require some knowledge about how to set it up and manage it.
So if you'd like a deep dive into multi-agent workflows and git work trees, let me know in the comments and I'll be sure to make one if there's enough demand.
This brings us to the end of the three recommended workflows that I use when developing with Claude Code.
Tips for Building Productively
And before we wrap up, I wanna share four helpful tips that I use for staying productive during the build phase.
Tip number one is to use the best models as much as possible. This means using the newly released Opus 4.5, or at least using sonnet as
much as you can Especially for important tasks where quality really matters.
Now since Opus 4.5 was released, I default to Opus for planning and complex tasks.
I then use Sonnet as an implementation workhorse and only use Haiku for simple, straightforward tasks and bug fixes.
The reason is simple. The time that I save by using a better model that makes fewer mistakes is more
valuable than the money saved from using a cheaper model that makes more mistakes that I have to spend more time fixing.
Plus, and this could just be me. I like to live on the edge and see the best of what these models are capable of.
So that's why I like to use Opus as much as possible. Tip number two is to periodically update and tune your Claude.md file.
Now, we might have set up our Claude.md file in the setup section, but as part of this build phase, I recommend periodically updating it as you add new features or
reach new milestones with your project. A pro tip here is that you can create a custom slash command to have Claude first
update your Claudemd file and then create a git commit as part of your git workflow.
This ensures that your documentation and code can stay in sync. Tip number three is to practice regression prevention.
When you see Claude make a mistake don't just fix it and move on. Instead, just type, hashtag or pound on your keyboard to give
Claude an instruction that it will then automatically incorporate into the relevant claude.md file.
This allows you to quickly update your Claude.md file on the fly without manual edits.
And finally, tip number four is don't be afraid to throw away work. Remember, code is cheap, so if something isn't working, especially in
the prototype stages, don't be afraid to undo it or throw away a feature completely and start again as this can often help you get to a solution that
you're actually happy with faster. Claude Codes. Checkpoints and rewind are very useful here.
It gives you session level recovery in addition to the project level version control that you get with git.
And that brings us to the end of the tips to keep you productive when building with Claude Code and to the end of phase three, the build phase.
Applying what you learned
Now if you wanna apply the system from this video and even get hands on help directly from me, I'm excited to announce my new course on Maven with cohorts
for January and February now open. And as a special thanks, I'm giving everyone who's watching this on YouTube,
a hundred dollars off the course by using the code YouTube at checkout, or using the link in the video description.
The AI native builder course is intense, but I promise it's worth it if you're serious about building With ai.
you'll build projects from scratch using tools like Claude Code and Replit, learn the fundamentals of building with AI that apply to any AI
coding tool and get personalized help when you're stuck with over 10 hours of q and a and office hours from me.
So check out the link in the video description and remember to use Code YouTube for a hundred dollars off.
And I have a limited number of scholarships available if you're super motivated, but cost is a hurdle.
You can find both the YouTube discounted link and the scholarship application in the video description.
Now, if you learn something from this video, don't forget to like and subscribe for more AI coding videos and leave a comment with what you learned
or with any questions that you have. I read every single one of them. Catch you in the next one.


