---
title: W5 Project Management
---
# Project Management

> [!tip] Project
> A project is a **temporary** endeavour undertaken to create a **unique** product, service, or result.

> [!tip] Project Management
> The **application** of knowledge, skills, tools, and techniques **to project activities** to meet the **project requirements**.
> 


# Work Breakdown Structure (WBS)
- A **deliverable-oriented** **hierarchical decomposition** of the work to be executed by the project team to accomplish project objectives and create the required deliverables.

![[Pasted image 20260928210649.png]]


## WBS Completion Checklist

### Appropriate Level of Detail
- Continue to **break the work down** until a task list is **developed** which meets the following criteria

> [!checklist] Criteria
> - [ ] **One and ONLY one** owner can be **assigned to** each of the **lowest level tasks**
> - [ ] **Clearly defined** outputs are evident for each task
> - [ ] **Quality can be monitored** through **performance criteria** associated with each output
> - [ ] The tasks **communicate the work** to be accomplished to the **person who is accountable**
> - [ ] The likelihood that a **task is omitted or work flow forgotten** is minimised
> - [ ] Each task is **well enough defined** and **small enough** so that estimates of duration are credible
> - [ ] The project is **broken down** to the level at which **you want to track**
> - [ ] As a general rule, the **lowest level tasks** should have durations between **2 and 20 days** and **effort** that equates to **not more than 1 person week**.

### No forgotten tasks
- Project delays are **often caused by forgotten tasks**, rather than inaccurate estimates.

### Ensure you have included tasks for
- **Planning** the project
- **Approval** cycles
- **Key project** meetings
- Management / Customer **interfaces**
- Quality inspections / fixing defects
- Training
- Management
- Test planning, development & execution
- **Project reviews** and **project closing**

![[Pasted image 20260928213111.png]]


# Planning & Estimating for Software Development

> [!tip] Why
> Before starting to **build software**, it is essential to plan the **entire** project effort in detail (as much as possible)

Planning **continues** throughout the project lifecycle
- **Initial** planning is not enough
- The earliest possible time that **detailed** planning can take place is **after** the **specifications** are complete

![[Pasted image 20260928213514.png]]


> [!tip] Cost estimate during requirements ($1M)
> - Likely **ACTUAL** cost is in the range ($0.25M, $4M)

> [!tip] Cost estimate at the END of the requirements ($1M)
> - Likely **actual cost** is in the range ($0.5M, $2M)

> [!tip] Cost estimate at the END of the analysis workflow ($1M)
> - Likely **actual cost** is in the range ($0.67M, $1.5M)

> [!important] Note
> The cost estimation at the **START** of the project will have a **BIGGER range** compared to during the **Implementation phase**.
> 
> The **more information** you have the **better cost estimation** you will have


## Accurate Duration Estimation is Critical
- Lose credibility, lose money or lose the contract

> [!tip] Note
> If you **over estimate** the duration, you will **waste manpower** and opportunity where you could have use those **resources on better things**.


## Accurate Cost Estimation is Critical
- Lose money or lose the contract

> [!tip] Note
> If you **OVER estimate** the cost the extra money deployed could have been **used on better things**


![[Pasted image 20260928214407.png]]



# Software Estimation

- Estimation of Size
- Estimation of Effort

## Size Estimation 

![[Pasted image 20260928214500.png]]

## Size Estimation: "How to" approach
1. **Decompose** the problem into **smaller** problems before estimating
2. What are the **metrics** for **measuring size** ?


# Size Estimation

- Function Points (FP)
- Use Case Points (UCP)
- Line of Code (LOC)

## Use Function Points to Estimate

> [!tip] Function Point Definition
> **Standard unit** for **measuring the size** of an **application system** based on the **functional view** of the system


![[Pasted image 20260928214755.png]]

## Steps

1. Compute **Unadjusted Function Points** (UFP)
2. Compute the **Technical Complexity Factor** (TCF)
3. Calculate the number of **Function Points** (FP)


# Determine the number of Unadjusted Function Points

> [!tip] How to Calculate
> - **inputs** (input screens, dialog boxes, tables, form submissions)
> - **outputs** (output screen, model displays, reports, output files)
> - **inquires** (search request)
> - **master files/logical files** (user data or control information)
> - **interfaces** (remote databases, cloud-based apps..)

- For each type of components you need to identify the number of **Simple / Average / Complex** type of component
![[Pasted image 20260928215141.png]]

> [!important] What is this ^
> This is the **weighted matrix**, how **complex** is each component.

## Figure out the functions for each component

- For "Input item", there are **3 functions**
	- User enters new items into the system (Simple)
	- User enters a sale transaction (Simple)
	- Another system sends over a new data (Simple)
- For "Output item" there are **2 functions** with "Simple Complexity"

![[Pasted image 20260928215502.png]]

> [!tip] How to Use
> Take the **number of Functions** \* Weight Matrix
> 
> Then **Sum up** all the points to get your **UFP**


## Technical Complexity Factor

> [!tip] Technical Complexity Factor
> Assign a value from 0 ("Not Present") to 5 ("Strong Influence throughout") to **each of 14 factors**.

![[Pasted image 20260928215833.png]]

> [!tip] Note
> Here `0.65` & `0.01` are **given**.
> 
> You only need to calculate the **Degree of Influence** then **compute** the **Technical Complexity Factor**

### What is the Source of the Values
- General data from **statistics**
- Accumulate your own **history** data
- **Adjust** the values accordingly


# Function Point Analysis

$$
FP = UFP * TCP
$$

### Example
$$
FP = 50 * 0.92 = 46
$$

### Unadjusted Function Points
- Representing the **functional requirement**
	- What the software **should do**

### Technical Complexity Factor
- A number between **0.65 and 1.35**
- **Adjusting** the number of function points **based on** the **relative complexities** of the project


# Use Case Points (UCP)

> [!tip] When to Apply Use Case Points
> We want to estimate **early in the project** based on Use Cases
> 

> [!example] For Example
> - Consider your team project, do you have the **necessary details** to count Functional Points (FP) at **week 2** ?
> - The **likelihood** is you **don't have the necessary details** to count Functional Points (FP)
> - We will then use **Use Case Points**


## Calculating Use Case Points

![[Pasted image 20260928220801.png]]

> [!important] How to read the thing
> On the **left**, are all the **Complexity**
> 
> On the **right** is all the **Non-Functional / Non-technical**
## Given a use case and assuming it has all its scenarios

> [!tip] Identify Transactions in a Use Case
> Transactions are not necessarily steps in a use casse
> - A transaction is a roundtrip from **User** to **System** to **User**

![[Pasted image 20260928220935.png]]

![[Pasted image 20260928220945.png]]


# Determine the Complexity of the Use Case

![[Pasted image 20260928222120.png]]

> [!tip] Note
> This weight matrix is also **given**.

![[Pasted image 20260928222203.png]]

> [!todo] Calculation
> We take the **no. use cases** we have then we **\*** with the **weight of the complexity** to get the **Unadjusted weight of Use Case**

## Identifying Actors

### Actors can be
- Users interacting through **Graphical User Interface**
- Users interacting through a **command line** (Text based)
- Components interacting through well define **API**
- Components or systems interacting **through protocols** (HTTP, SOAP, TCP/IP, etc)

![[Pasted image 20260928222525.png]]


### Calculating All Actors in Our Case Study

![[Pasted image 20260928222604.png]]


## Determining the Technical Complexity Factors

> [!tip] Definition
> **Factors** that could **influence the development** of the software
> 
> The weight here represents the impact of such factor. **This is given to you**
> - Developers should **assess the importance** of each **factor** on their project

![[Pasted image 20260928222830.png]]

![[Pasted image 20260928222844.png]]

> [!tip] Note
> The `0.6` and `0.1` is given, we only need the **Degree of Influence** to calculate the **Technical Complexity Factor**


## Environmental Factors

> [!tip] Why do we need to calculate this ?
> There are **several factors** in the **development environment** that could **affect the size** of a project

![[Pasted image 20260928223235.png]]


## Calculating Environmental Factors
![[Pasted image 20260928223304.png]]

> [!important] Note 
> Here the **scale** is from 0-5
> 
> REMEMBER: Part time Workers & Difficult Programming Language are **NEGATIVE**

![[Pasted image 20260928223359.png]]


## Calculating Use Case Points

![[Pasted image 20260928223407.png]]



# Estimation of Effort

> [!tip] Why do we need to estimate effort
> - **Cost** of the project and **Time** to complete the project is predicted by **estimating efforts**.

## COnstructive COst MOdel: COCOMO

- Uses **empirically derived** formulas to predict effort
	- Input: **Use Case Points** (UCP), Line of Code (LOC), etc...
	- Output: The **effort** in months/hours of work for **1 person**

## Effort estimation using Use Case Points

> [!warning] Scenario
> - The creator of **UCP** has given the **following range** of **estimation of hours** for **each UCP**: 15-30 hours
> - The **estimated effort** in developer-hours of a project of size **450 UCP** falls between

$$
(15-30) * 450
$$
- This isn't what we want because it still does not give us an estimate on how much effort or time it takes to complete.

## Estimate Task Duration

- Optimistic Duration (OD): Minimum amount of time to perform task (Lower Bound)
- Pessimistic Duration (PD): Maximum amount of time to perform task (Upper Bound)
- Expected Duration (ED): Average amount of time to perform task (Upper + Lower / 2)

- Weighted average of the most likely duration(D) is:

$$
D = \frac{(1 * OD) + (4 * ED) + (1 * PD)}{6}
$$














