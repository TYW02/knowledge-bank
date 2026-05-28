---
title: AI in Organizations Today
tags:
  - AI
  - AI_Guardrails
  - AI_Risk
  - Prompting
---

# Every AI tool does 1 of 3 Jobs

## General Assistant
Language, Thinking, and knowledge tasks (ChatGPT, Claude, Gemini)
- Draft - Emails, reports
- Analyze - Summarize research, find patterns in data
- Think - Brainstorm, stress-test ideas
- Explain - Simplify complex topics for any audience


## Coding assistant
Write, Review, Test, and fix code faster (Github Copilot, Cursor, Claude Code)
- Generate - Boilerplate, functions, SQL queries
- Debug - Explain errors, suggest fixes in context
- Test - Write test cases and edge cases automatically
- Review - Spot logic gaps and security issues in PRs


## Workflow assistant
Connect Tools, automate tasks across System (Notion AI, M365 Copilot, Zapier AI)
- Connect - Sync emails , tasks, Slack automatically
- Automate - Fill spreadsheets from form input
- Summarize - Condense long slack threads or meeting transcript
- Embed - AI inside the tools your team already uses daily

# Pick the right AI role
- Analyst - Find themes and trade-offs
- Critic - Find risks and weak assumptions
- Simulator - Predict stakeholder reactions
- Project Manager - Turn ideas into tasks and owners
- Test Designer - Find edge cases and acceptance criteria
- Security Reviewer - Spot privacy and access risks



# Good Prompting
#Prompting

Don't expect AI to give you good output if you say "Give me an answer"

## Instead follow TCREI:
Task - What do you want done ?
Context - Audience, data, goal, background
Requirements - Constraints and output format
Examples - What good or bad looks like
Iteration - How to check, revise, or ask questions

### Example

Weak: "Explain APIs"
Better: "Explain REST APIs to non-technical audience using a food ordering app analogy"
Strong: "Explain REST APIs using a campus food ordering app. Include 1 example endpoint, one request/response example, 1 common error, and 1 security check before using the API"


# Enterprise Adoption
**Most pilots never become real**
1. Hero use case
"Pick 1 visible pain"
Find a problem that is undeniable and a result is measurable

2. Pilot
"Test with real users"
Run with actual data, real constraints, and people who do the jobs NOT a demo environment

3. Workflow
"Embed, don't bolt on"
Redesign the process AROUND AI, If you can remove the AI and nothing changes, it's not embedded

4. Measurement
"Measure what matters"
Track quality, speed, risk and adoption not just usage. Vanity metrics kill good programmes

5. Governance
"Controls before scale"
Logs, policies, escalation paths, and ownership. You can't govern what you don't understand.

6. Scale
"Expand what works"
Apply the embedded model to adjacent workflows, Budget, training, and clear ownership make it stick

# Risk and Guardrails
#AI_Guardrails

> [!warning] Accuracy
> Hallucinated facts, citations, and policies. Stated with full confidence
> ```
> Verify every claim. AI is first draft, not a final answer
> ```

> [!Context Gap]
> AI optimises for the general case. It doesn't know your org, market or constraints
> ```
> Inject local context explicitly: industry, policy, constraints
> ```

> [!Bias]
> Training data encodes historical inequalities. AI can amplify them at scale.
> ```
> Audit outputs for patterns. Never use AI as sole decision-maker for people
> ```

> [!danger] Privacy
> Data entered into AI tools can be logged, retained, or exposed.
> ```
> Classify data first. Enterprise-grade tools with DPA agreements only.
> ```

> [!Security]
> Agentic AI that takes actions introduces prompt injection and access risks.
> ```
> Least privilege access. Log all actions. Human approval for irreversible steps
> ```

> [!success] Accountability
> When AI gets it wrong, organizations often can't say who is responsible or why.
> ```
> Humans own every decision. Document model, prompt, and reviewer.
> ```

### Ask yourself these questions before you deploy:
- Can I verify the output ?
- Did I give enough context ?
- Could this harm someone ?
- Is sensitive data involved ?
- Who is accountable ?


# Risk Ladder
#AI_Risk

## Low Risk
- Brainstorming
- Formatting
- First draft
- Practice questions
**Check Lightly**

## Medium Risk
- Project analysis
- Coding help
- Stakeholder summaries
- Customer Themes
**Verify Evidence**

## High Risk
- Legal
- Medical
- Financial
- Cybersecurity
- Hiring
- Grading
- Access Decisions
**Require sign-off**

# Cost + Budget
> [!License + API]
> "Unlimited" plan still bill by usage. A poorly-optimized prompt loop can generate thousands of dollars in a week
> ```
> Set usage limits and alerts from day 1
> ```

> [!Integration]
> Connecting AI to real data, systems, and workflows typically costs 3-5x the license in engineering time.
> ```
> Budget integration separately. Not as an afterthought
> ```

> [!Controls]
> Privacy review, audit logging, and governance infrastructure aren't in any vendor quote. They're a separate project.
> ```
> Skipping controls isn't cheaper. You just pay later, after an incident
> ```

> [!Optimization + Training]
> Not every task needs GPT-4. Routing by model complexity cuts API spend 60-80%. Change management is the hidden human cost.
> ```
> Optimization and training are where ROI is won or lost
> ```

