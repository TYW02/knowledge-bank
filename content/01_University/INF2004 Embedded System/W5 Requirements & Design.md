---
title: W5 Requirements & Design
---

# Why Clear Requirements Matter

- Defines '**What**' the software **MUST DO** (**NOT HOW**)
- Prevents **Costly Redesign**
- Must include **Hardware Specification**, **Real-time Constraints**, **Safety requirements**
- **Traceability** to tests ensures validation
# Requirements Overview

## Anti-Patterns
- Requirements **aren't written** down
- Requirements **incomplete**, **imprecise**
- "Be like last version, except"

## Requirements
- Requirements **faults** can **defeat a design** before it is even built
- **Describe** what system does
	- Also what it's **not supposed** to do
- Precise, **testable** language
	- Each requirement **traces** to system test

### Requirements issues
- Requirements **not defined** when **development contract signed**
- "We will know it when we see it"
- **Repeated** requirements changes
- **Scope creep** (new requirements added) of 80%


# The Art of Requirements: Spectrum of Detail

> [!error] Send readings regularly

> [!warning] Transmit a reading every minute

> [!success] Transmit an encrypted sensor reading every 60 +- 1s, with a minimum end-to-end reliability of 99%

## Why This Matters: Traceability

> [!Definition] Definition
> A **well-written requirement** is the **cornerstone** of a structured development process. It enables **traceability**, which is the ability to f**ollow a requirement through every stage** of the lifecycle.

> [!tip] Requirement
> The "**WHAT**" the system **MUST DO**

> [!tip] Design
> The "**HOW**" the system will **meet the requirement**

> [!tip] Testing
> The evidence that the "**WHAT**" and "**HOW**" were **correctly implemented**

- Without a **clear and measurable requirement**, there can be **no definitive design** or test case, making it **impossible** to **prove** that the system **performs as intended**


# Characteristics of Good Requirement

> [!tip] Clear & Focused
> - **Precise**, **concise**, and **minimally constrained**
> - States **what** the system must do, **not how** to do it
> - Uses **consistent terminology**

> [!tip] Verifiable
> - Written with "**shall**" (**mandatory**), "**Should**" is only a **goal** and **cannot fail a test**
> - Where possible, includes **numeric targets** with **tolerances** (e.g. 500 ms +- 10%, less than X)
> - Requirement satisfaction can be **tested** with a **clear yes/no outcome**

> [!tip] Traceable
> - Each requirement has a **unique ID**
> - Cleanly **maps to a test**

> [!tip] Justified & Coherent
> - Supported by **rationale or commentary**
> - Fits within the **overall system context**
> - **Conflicting requirements** are **resolved or prioritised**

# Problematic Requirements

> [!warning] Untraceable (No label)
> - The system must display the current room temperature on the LCD

> [!warning] Untestable
> - R-1.1: The thermostat shall **always** maintain a comfortable room temperature

> [!warning] Imprecise
> - R-1.2: The display should be **easily** readable

> [!warning] No Measurement Tolerance
> - R-2.1: The system shall update the temperature reading every 2 seconds.

> [!warning] Overly Complex
> - R-3.1: Pressing the 'up' button **shall** increase the temperature, **and** pressing the 'down' button should decrease it, **but if** the temperature is at its maximum, pressing the 'up' button **should** instead turn on the backlight, **which** can also be turned on by pressing and holding the 'mode' button for 3 seconds

> [!warning] Describes Implementation
> - R-4.1: The system shall read the temperature from the **LM35 sensor** via the **I2C bus** and store the value in a **signed 16-bit** integer before displaying it on the **LCD**

# Non-Functional Requirements

> [!tip] 1.Emergent Properties
> - System-level qualities, **not tied** to a **single component**
> - Examples: Performance, reliability, dependability
> - Often **verified** at the **overall system boundary**

> [!tip] 2.Perfomance & Timeliness
> - Throughput, latency, response time
> - **Real-time deadlines** and **scheduling guarantees**

> [!tip] 3.Safety, Security & Dependability
> - **Negative** requirements ("System shall not...")
> - **Safety mechanisms** to prevent or mitigate hazards
> - Many behaviours are **emergent** and **require system-wide assurance**

> [!tip] 4.Resource Constraints
> - Size, Weight, and Power consumption **limits**
> - **Allocated** as a budget **across subsystems**

> [!tip] 5.Design & Project Constraints
> - Compliance with **standards** (e.g. ISO 26262, DO-178C)
> - **Mandated** technology or platform choices
> - **Business constraints**: cost ceilings, deadlines, staffing


# Product vs Engineering Requirements
![[Pasted image 20260927191341.png]]

## Requirement Approaches

> [!tip] Text Document
> - Simple **list of requirements**
> - **Works well** if domain experts **know what they want**
> - **Improves** over time

> [!tip] UML Use Cases
> - Show **activities** performed by **actors**
> - Requirements **expressed as scenarios** attached to each use case

> [!tip] Agile User Stories
> - Each story = 1 small piece of **user value**
> - Format: "As a \[user\], I want \[goal\], so that \[benefit\]"

> [!tip] Functional Decomposition
> - Start with **main system functions**
> - Break into **detailed sub-functions**
> - Builds a "Functional Architecture"

> [!tip] Prototyping
> - Customers **recognise needs** when they see it
> - Paper mock-ups can help **refine requirements**

![[Pasted image 20260927191731.png]]


# Wrap-up & Preview
- Good requirements are the **backbone** of **design and testing**
	- Clear & Focused, Verifiable, Traceable, Justified & Coherent
- Say **what** and **how well**, **never how**: Give every requirement an **ID** and every number a **tolerance**


# Architecture to High Level Design (HLD)

- Product Requirement (PR): What the **user/business wants**
- Software Requirements Specification (SRS): What the **system must do in detail**
- High-level design (HLD): How the system will be **organised to meet those requirements**
	- Architecture: The structure inside the HLD (Components + Interfaces)

> [!tip] What Each Diagram Show
> - Architecture: Boxes & Arrows (**Interfaces**)
> - HLD = Architecture (**nouns**) + Sequence Diagrams (**Verbs**)
> - Sequence Diagrams (SDs) show **time-based interactions**
## Common Mistakes
- **Skipping** Requirements -> Code
- **No visual representation** of how all components fit together
- Diagram that **omits interactions**

## Software Architecture

- Boxes: **Software modules**
- Arrows: **Interfaces**

- Each box/arrow has **meaning**
- Give every box and arrow an **ID for traceability**
- Ideally, **entire architecture** should be represented on a **single page**
- OK to have **sub-systems**

### Other Types of Architecture Diagrams
- System Architecture
- Hardware Architecture with Software Allocation
- Data Architecture

![[Pasted image 20260927192558.png]]


![[Pasted image 20260927192605.png]]


![[Pasted image 20260927192611.png]]

![[Pasted image 20260927192621.png]]


# Best Practices

> [!tip] Use Case to Diagram
> 1. Start with **Clear Use Cases**
> 2. Scenarios
> 3. Sequence Diagrams
> 4. Unified Statechart


> [!bug] Common Pitfalls
> - Missing interactions in diagrams
> - Undefined meaning for boxes/arrows
> - Mixing HLD with detailed design (Keep separate per component)


# Key Takeaway

> [!task] HLD & Architecture
> - Show **all parts** of the system, **how they connect**, and **how they work together**
> - Use **clear names** for things (**nouns**) and their actions (**verbs**)
> - **Don't mix** big-picture design with detailed coding stuff (**Keep them separate**)
> - If you **leave things out** or **duplicate** them, it will **cause problems later**

> [!task] Sequence Diagram
> - Draw 1 diagram for **each situation** (**Normal** and **Error** cases)
> - Show clearly **what goes in**, **what comes out**, and where the system **starts and ends**
> - If you **leave out steps**, you might **miss important requirements later.**

> [!task] Statecharts
> - Combine **all scenarios** into 1 **big picture of system behavior**
> - Helps find
> 	- **Missing** steps
> 	- **Unclear** details
> 	- **Duplicate** or **conflicting** actions
> - Use **grouping** (**hierarchy**) and **parallel paths** (**Concurrency**) to keep things **simple**
> - **Review** and **improve often**, combining everything shows problem early.
















