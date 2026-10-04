---
title: W1 - W5 Notes
---


## WEEK 1: Intro to SE & SDLC

**Software engineering:** systematic, disciplined, quantifiable approach to development, operation and maintenance. Dual emphasis: **product** (what is produced) and **process** (how). **Fault:** software behaviour unaccounted for in its design.

### Cost facts

|Fact|Value|
|---|---|
|Maintenance share of total cost|**67%**|
|Corrective / Perfective / Adaptive (post-delivery)|**~20% / ~60% / ~20%**|
|Perfective + Adaptive|"Enhancement"|
|Cut coding cost by 10%|at most **2%** total saving|
|Cut post-delivery maintenance by 10%|**6-7%** total saving|

**Fault fixed EARLY:** usually just a document changes. **Fault fixed LATE:** change code + docs, test the change, regression testing, reinstall on client machines. **New coding method 10% faster, adopt it?** Consider training cost, impact of new technology, effect on maintenance.

> [!important] **Case studies:** 
>  California DMV (huge overruns, cancelled). BBC DMI: scrapped due to bad management and being outpaced by technology; cheaper **COTS** (Commercial Off The Shelf) alternatives existed.

### Models: when to use / not to use

|Model|Key traits|Use when|Do NOT use when|
|---|---|---|---|
|**Waterfall**|Sequential, distinct phases, document-driven, BDUF (Big Design Up Front). No working product until the end.|Requirements well known, tech understood, new version of existing product, small/simple, regulated gov projects|New idea, new/unknown tech, strict timeline/budget, complex long-term, maintenance projects|
|**Rapid Prototyping**|Linear. Replaces requirements with: listen, build prototype, customer test-drives. Customer sees real product only at end.|Requirements unclear|Never turn prototype into product. May replace **specification**, **never design**|
|**Spiral**|4 phases, iterative, **risk analysis every iteration**, radius = **accumulated cost**, customer involved throughout|High-risk, large systems, totally new ideas|Client not available, urgent progress, strict timeline/budget, **low-risk/low-budget**|
|**RUP**|Phases: **Inception, Elaboration, Construction, Transition**. Use-case & architecture centric, tied to UML, adaptable framework|Medium-large projects, strict budget/schedule, need value early|**Small simple projects**, limited budget|
|**Agile**|Fixed **timebox** (1-4 weeks), "fixed time, not fixed features", descoping, velocity, customer involvement (not _during_ iterations), light documentation|Small-medium, changing requirements, new tech, time-critical|Poor team, large projects needing formal docs, large systems that cannot be modularised|

- **Waterfall cons:** needs precise requirements, no working model until end, high risk, hard to change.
- **Rapid prototyping challenges:** throw-away phenomenon, demos set unrealistic expectations, compromises solidify. 
- **Spiral cons:** long iterations (0.5-2 yrs), lots of docs, needs risk experts, high cost. 
- **RUP cons:** complicated, expensive tools, only medium/large, heavy documentation. 
- **Agile cons:** possible rework, needs close client collaboration, needs good automation tools, needs trust.

### RUP phases

|Phase|Focus|
|---|---|
|**Inception**|Initial business case, tentative schedule/budget, risk assessment, understand domain. Usually short.|
|**Elaboration**|Refine requirements/use cases, architecture, business case, project plan|
|**Construction**|Implementation + testing (integration, product testing). Usually longest.|
|**Transition**|Move to customer's real environment, correct faults, complete manuals|

### Agile manifesto (value LEFT over right)

Individuals & interactions > processes & tools · Working software > comprehensive documentation · Customer collaboration > contract negotiation · Responding to change > following a plan. Agile methods: **Scrum, Kanban**.

---

## WEEK 2: Requirements Engineering

**Moving target problem:** requirements change while the product is being developed. Consequences: **regression fault** (fault in an unrelated part), possible full redesign. Fix: spend effort at the requirements stage. Why requirements change: stakeholders know what they _want_, not what is _required_; varied domain expertise; requirements evolve as understanding grows.

### 4 RE activities

|Activity|Key question|
|---|---|
|**Elicitation**|Discover what stakeholders _need_ (not just want). Focus on the problem, not the solution|
|**Analysis**|Refine and extend requirements|
|**Validation**|"Are we building the **right** product?"|
|**Management**|Manage changing requirements|

### Analysis vs Validation (memorise!)

|ANALYSIS activities|VALIDATION|
|---|---|
|**Categorisation** (functional vs non-functional)|**Reviews & walkthroughs**|
|**Prioritisation** (MoSCoW)|**Prototyping**|
|**Conflict resolution** (incompatible wants)|**Test-case generation**|
|**Feasibility analysis** (technical, cost, schedule)|Checks: **Validity, Consistency, Verifiability, Realism, Completeness**|
|**Dependency analysis** (which depends on which)||
|**Modelling** (use cases, activity diagrams, etc.)||

Trap: Feasibility (analysis activity) vs **Realism** (validation check). Consistency = "conflicts?"

### Stakeholders

|Group|Examples|
|---|---|
|**Primary**|End-users, product owners/clients, system administrators|
|**Secondary**|Managers, customer support, marketing & sales|
|**External**|Regulators, investors, competitors|
|**Internal**|Developers, testers, UX/UI designers, project managers, QA|

### Elicitation techniques

|Technique|Pros|Cons|
|---|---|---|
|**Interviews** (structured / unstructured / **semi-structured**)|Deep insight, instant clarification, hidden needs|Time-consuming, hard to scale, bias|
|**Focus groups** (6-12 people, moderator)|Brainstorming, shows **conflicting priorities**|**Groupthink**, dominant voices|
|**Existing documents**|Objective, saves time|Outdated, may not reflect real practice|
|**Observation** (passive / active-participant / **shadowing**=whole workday)|Real practice, workarounds|Time-consuming, **Hawthorne effect**|
|**Prototyping** (throwaway/rapid vs **evolutionary**; low/high fidelity)|Makes needs concrete|Costly, confused with final product|
|**Questionnaires**|Large audience, cheap, quantifiable, anonymous|Shallow, low response, no clarification|
|**Scenarios** (actors, context, goals, steps, exceptions)|Reveals exceptions and alternative flows|Can oversimplify|

### Functional vs Non-functional

- **Functional = "WHAT"** (tasks the system performs). **Non-functional = "HOW WELL"** (reliability, security, usability, performance, constraints).
- NFR types: **Product** (performance, reliability, security) · **Organisational** (policies, e.g. "authenticate using ID card", coding standards) · **External** (regulatory, legislative, ethical, e.g. "privacy law").
- "Should be secure / fast / easy to use" = non-functional and **not verifiable**. Rewrite with measurable numbers.

### 7 characteristics of a good requirement

1. **Verifiable** (testable) 2. **Clear & Concise** (single requirement, no multiple interpretations) 3. **Traceable** (unique ID) 4. **Viable** (technology, budget, schedule, skills) 5. **Consistent** (no conflicts, same terms) 6. **Implementation Free** (no technology choices, e.g. "use Oracle") 7. **Complete** (no guessing: units, how long, 50% of what)

### MoSCoW

**M**ust-have · **S**hould-have · **C**ould-have · **W**ill-not-have (excluded from current scope)

### Specification formats

|Format|Notes|
|---|---|
|**Natural language**|Numbered sentences, one requirement each. Problems: lack of clarity, mixing, confusion|
|**Structured natural language**|**Standard form**: inputs, outputs, pre/post-conditions, side effects|
|**Formal**|Mathematical (finite-state machines, sets). Unambiguous but needs experts; customers can't read it|
|**Graphical**|UML use case, sequence diagrams + text|

**SRS** = Software Requirements Specification (IEEE: correct, unambiguous, complete, consistent, verifiable, modifiable, traceable).

---

## WEEK 3: Use Case & Activity Diagrams

### Use case basics

- Use case = how an actor interacts with the system to achieve a **goal**. Covers **functional** requirements only (**NFRs are NOT use cases**).
- Name use cases as **goals**: _Borrow Book_, _Pay Fine_ (not "System shall...", not "click button").
- **Primary actor** initiates. **Supporting actor** performs sub-goals (e.g. payment system, bank database). Actors need not be human; the **system itself is not an actor**.
- Good use case: starts with an actor's request, ends with all answers; from actor's view; no internal activities, no GUI details.

### Diagram notation

|Element|Symbol|
|---|---|
|Actor|Stick figure|
|Use case|Ellipse|
|System boundary|Rectangle enclosing use cases|
|Association|Line|

|Relationship|Meaning|
|---|---|
|`<<include>>`|**Mandatory**. Base always runs it. Extracted for **reuse** (e.g. Validate PIN)|
|`<<extend>>`|**Optional/conditional**. Extending use case adds behaviour only under conditions (e.g. Report Forgery extends Validate ID Card)|

### Use case description template (fill EVERY field)

**ID** · **Name** · **Description** · **Primary Actor** (+ supporting) · **Preconditions** (true BEFORE start) · **Main Success Scenario** (numbered steps) · **Alternative Scenarios** (numbered 2a, 2a1... incl. exceptions) · **Post-conditions** (system state AFTER: main + alternatives) · **Priority** · **NFR** (if any) Post-conditions are **states** ("Booking is cancelled"), not actions. Give **both** main and alternative if asked.

### Activity diagram nodes

|Node|Shape|Use|
|---|---|---|
|Start|Filled circle|Begin|
|Activity|Rounded rectangle|Verb phrase ("Validate payment")|
|**Decision**|Diamond|**One** path chosen; guard conditions on arrows|
|**Merge**|Diamond|Brings **alternative** (decision) paths back together|
|**Fork**|Thick bar|Splits into **parallel** activities|
|**Join**|Thick bar|**Waits for all** parallel flows|
|End|Bullseye|End|

Pairs: **Decision -> Merge** (one path) · **Fork -> Join** (all paths at once). Disadvantage: doesn't show **which objects** execute activities or how they message.

---

## WEEK 4: Class & Sequence Diagrams

**Class** = template (attributes + services). **Object** = instance of a class. **Entity classes:** long-lived, data-bearing business objects. OO benefits: reuse, maintainability, good design, understandable.

### Use case -> classes (4 steps)

1. Write **Solution Abstract** 2. **Filter nouns** 3. Determine **attributes & services** 4. Derive **relationships**

### Noun filtering (give a REASON for EVERY excluded noun)

|Exclude|Why|Becomes|
|---|---|---|
|Outside problem boundary|e.g. _system_, _building_, a location|nothing|
|**Abstract nouns**|e.g. _movement_, _illumination_, _fine_, _date_, _time_|attribute or service|
|Events/verbs mistaken as nouns|e.g. _scan_, _register_|service|
|A class can be a tangible entity, abstract entity, **role**, or **event**. Don't drop obvious classes (e.g. Book, Loan, Appointment). Stay consistent between exclusion list and class list. Always list **all nouns** (including "system").|||

### Visibility

|Symbol|Meaning|
|---|---|
|**+**|public (everyone)|
|**-**|private (own class only)|
|**#**|protected (class, subclasses, same package)|

### OO principles

|Principle|Meaning|
|---|---|
|**Encapsulation**|Group data + functions, selectively hide attributes/operations|
|**Inheritance**|Reuse higher-level class spec; **"is a"** (Duck is an Animal)|
|**Polymorphism**|Same message, different implementations, transparent to client|
|Info hiding|Internal state not directly accessible|

**Constructor** = creates instance · **Mutator** = alters state (`setX`) · **Accessor** = reads state (`getX`). Bad design: one Animal class with a `Type` attribute and `if` checks (grows huge, keeps changing). Elevator case: buttons don't talk to elevators directly, so add **Elevator Controller**. Super-class **Button**, sub-classes **ElevatorButton**, **FloorButton**. Tool for class diagram content: **PlantUML**.

### Sequence diagram

- **Horizontal** = which participant acts. **Vertical** = time (downward).
- **Lifeline** = dashed vertical line. **X** at bottom = deletion. Created mid-scenario = lower, arrow labelled **'new'**.
- **Message** = solid arrow; **return** = dashed arrow. **Activation** = thick box on lifeline.
- Frames: **opt** (if) · **alt** (if/else, dashed line) · **loop** · **ref** (refer to another diagram).
- Useful because: language-agnostic, non-coders can read, easier as a team, many objects on one page.

---

## WEEK 5: Project Management & Estimation

**Project:** temporary endeavour to create a unique product, service or result. **WBS:** deliverable-oriented hierarchical decomposition of work. Lowest-level tasks: **2-20 days**, effort **<= 1 person-week**. Delays often come from **forgotten tasks**. **Cone of Uncertainty:** estimate range narrows as information grows. $1M example: requirements start 0.25M-4M -> end of requirements 0.5M-2M -> **end of analysis 0.67M-1.5M** (earliest appropriate time for detailed estimate). Keep re-estimating throughout. **COCOMO** = **Co**nstructive **Co**st **Mo**del. LOC criticism: only accurately known after completion, differs by language.

### PERT duration

```
D = (OD + 4*ED + PD) / 6        ->  add the WHOLE numerator first, then divide once
```

Example: (3 + 4*8 + 19)/6 = 54/6 = **9**

### Function Points (FP)

|Component|Simple|Average|Complex|
|---|---|---|---|
|**EI** External Input|3|4|6|
|**EO** External Output|4|5|7|
|**EQ** External enQuiry|3|4|6|
|**ILF** Internal Logical File|7|10|15|
|**EIF** External Interface File|5|7|10|

```
UFP = sum(count x weight)
TCF = 0.65 + 0.01 x DI        (14 factors, range 0.65 to 1.35)
FP  = UFP x TCF
```

### Use Case Points (UCP)

|Use case (transactions)|Weight|
|---|---|
|Simple (**<= 3**)|**5**|
|Average (**4-7**)|**10**|
|Complex (**> 7**)|**15**|

|Actor|Weight|
|---|---|
|Simple (API/component)|**1**|
|Average (protocol/external system)|**2**|
|Complex (human using GUI)|**3**|

```
UUCW = sum(weight per USE CASE)      <- weight is per use case, NOT x number of transactions
UAW  = sum(count x actor weight)
TCF  = 0.6 + 0.01 x DI          (13 factors)    <- NOT 0.65!
EF   = 1.4 + (-0.03 x DI)       (8 factors)     <- EF = 1.4 when DI = 0
UCP  = (UUCW + UAW) x TCF x EF  <- brackets around the sum
Effort (hours) = UCP x hours-per-UCP     (range 15-30 hours per UCP)
```

**Worked check:** UUCW 65 + UAW 10 = 75; TCF = 0.6+0.3 = 0.9; EF = 1.4-0.3 = 1.1; UCP = 75 x 0.9 x 1.1 = **74.25**; at 20 hrs/UCP = **1,485 hrs**.

---

## QUICK EXAM HABITS

1. **Re-read the first line** of every question; answer exactly what is asked.
2. **Count the parts** (e.g. "2 reasons + 1 weakness", "two alternative scenarios", "main AND alternative post-condition") and tick each off.
3. Use the **exact slide terminology** for one-word answers (Lifeline, Semi-structured, Timebox, Formal specification, Constructor, Dependency analysis).
4. In calculations: write formulas first, **bracket sums**, double-check **TCF 0.65 (FP) vs 0.6 (UCP)**.
5. Give a **reason for every** noun you exclude.
6. Don't confuse similar pairs: Feasibility vs Realism · Merge vs Join · Fork vs Decision · Accessor vs Mutator vs Constructor · Primary vs Secondary stakeholders.