---
title: Claude Code 101
tags:
  - Skills
  - Context
---
# 3 Concepts to keep in Mind
Context Window: Claude's working memory. It can hold a lot but not everything at once. Claude find strategic ways to locate answers within your codebase without loading the entire thing into context.

It asks for permission: Claude Code will ask for permission before running commands or making changes.

It can make mistakes: It might misunderstand intent, introduce bug, or over-engineer a solution

# The Agentic Loop
1. Enter a prompt into Claude Code
2. Claude gathers context it needs, which returns text or tool call that it executes
3. It takes action, editing file or running command
4. Verifies results and determines whether they achieve what your prompt set out to do
5. If they do, Claude finishes and waits for next prompt. If they don't it loops back and tries again until results are complete and verifiable.

## Context
#Context
Determines how much of your conversation, file content, command outputs, it can store and reference. Once you hit the limit, Claude compacts your conversation, automatically determining what it can remove or summarize to resize the context window.

## Tools
Tools let Claude determine *when* to execute code to get closer to completing a task. This could be file-reading, web search etc...


## Permissions
Default Behavior: Asks for explicit permission before editing file or running shell command
Auto-accept: Files are edited without asking, but commands still require approval
Plan Mode: Uses read-only tools to compile a plan of action before starting work.


# Workflow
> Explore -> Plan -> Code -> Commit


## Explore and Plan
Go into plan mode.
Claude will read relevant files, run web searches, and give you a plan of action. Review it and decide if it meets your criteria. If not, ask it to revise specific areas.

This is the best place to course-correct because it's before any code it written.

## Code
Tips to make coding phase smoother:
- Define success criteria: Be clear on what "Correct" looks like. Make it explicit when writing your plan
- Add tools: Tools that help Claude complete its goals remove a lot of back and forth
- Include a test suite: Give Claude a test suite it can continuously validate against.


# What Happens when context fills up ?
Context window is automatically compacted. Compaction summarizes important details and remove unnecessary tool call results to free up space.

> [!NOTE]
> This process can potentially lose details


# Commands
You can run compaction manually with `/compact`. It's handy when you want to free up context space while keeping a memory of what you previously worked on.

If you want to completely start from scratch with no memory of the previous session, run `/clear` 

To check the state of your context, run the `/context` command. You'll get a high-level overview of your context size

## When to use
- Use `/compact` when working on a specific feature and running up against the context limit but need to continue
- Use `/clear` when you want to start a new feature. You don't want the previous conversation to introduce bias into something new. For things you want to remember across sessions, put them in `CLAUDE.MD` so it doesn't have to rediscover from scratch

## Tips for Saving Context Space
- Be specific: Without clear instructions Claude is forced to explore your codebase more and do its own reasoning
- Manage your MCP servers: MCP servers load ALL tools into context by default, even when you're not using them.
- Use subagents: Subagents run in parallel with your main agent but have a completely separate context window. For simple tasks your subagent does the work and returns a summary to your main agent, keeping primary context clean.


# CLAUDE.md
It's a markdown file you add to the root of your project, it is read automatically every time you start a session.

### Save corrections to memory
If you find yourself correcting Claude repeatedly, explicitly ask Claude to save that rule to memory

- Reference project docs: Use the `@` with file path to let Claude reference
- Start without one: Start a project without a CLAUDE.md to see where you have to course-correct the model. To keep your CLAUDE.md compact, when ready run `/init` to generate one.


# Subagents
Claude spawns a subagent to handle a task in parallel with its own context window, once finished it will summarize its findings and return that to Claude


## Creating Your own Subagent
Subagents are defined in Markdown files with YAML frontmatter or you can run`/agents`

### Further Customization
- Persistent Memory: Let subagent retain memory across conversation
- Preload skills: Unlike your main conversation, the entire skill is loaded into context here.


# Hooks
Let you run commands at specific points in Claude's lifecycle

## Common use cases:
- Auto-formatting after file edits
- Logging all executed commands for compliance
- Blocking dangerous operations like modifying production files
- Sending yourself notification when Claude finishes a task

## How they work
Hooks are configured in `settings.json`

### Available Events
- PreToolUse: Runs before a tool call
- PostToolUse: Runs after a tool call completes
- UserPromptSubmit: Runs when you submit a prompt, before Claude processes it
- Stop: Runs when Claude finishes responding
- Notification: Runs when Claude sends a notification

