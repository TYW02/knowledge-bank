---
title: W4 Database Refinement
---
# What makes a Good Relational database design
- MUST **capture** ALL necessary **attributes** / associations
- With **MINIMAL** amount of stored information
- Minimal stored information = **less redundant**

## Redundancy
- Redundancy is generally a "**bad thing**"
	- Causes problem **maintaining consistency** after updates
	- Unnecessary data, **waste space**
	- Slow updates or Inconsistent Data
- Certain redundancy may give **performance improvements**
	- **Avoid join** to collect pieces of data together


## Database Refinement
- Refinement / Normalization
	- No **missing** information
	- Easy for information management, easy to **add constraints**
	- No **unnecessary** redundancy
		- Redundancy: **Repetition** of data or **duplicate** data stored in different location
		- Some redundancy **cannot be avoided**


# Anomalies
> Problem occurred on poorly planned databases

- Insertion anomalies: **NOT possible** to store information **unless** some other information is stored

- Redundant anomalies: Some information is **stored repeatedly**

- Update anomalies: If one data is updated, inconsistency is created **unless all data are updated**

- Deletion anomalies: **Not possible** to delete information **without losing** some other information

> [!Solution]
> Decomposition


# Decomposition

> Decomposing a larger relation into smaller relations

- Replacing relation schema by >= 2 schemas
- Each with a subset of the attributes
- These subsets together include all attribute

![[Pasted image 20260922212918.png]]


# Functional Dependency (FD)
> Association between any 2 attributes

- The non-key **attribute** is functionally dependent on the **primary key** attribute
- Denoted as X -> y 

> [!How to read]
> Attribute Y is **functionally dependent** on X.
> 
> X **determines** Y

![[Pasted image 20260922213132.png]]

> [!Note]
> Here Position determines Phone because the **SAME** position (**Salesrep**) returns you the **SAME** Phone (**9876**)
> 
> BUT Phone does **NOT** determines Position because the **SAME** phone (**1234**) does **NOT** return the **SAME** Position (**Clerk**, **Lawyer**)


A **legal** instance must satisfy ALL specified ICs, including FDs
- FD is a statement about all possible legal instances of the relation
- Looking at an **instance**, we may tell that a certain **FD does not hold** (As long as there is 1 instance where the FD does not hold)
	- We **cannot deduce** that an FD holds **just by looking** at 1 instance (We have to see **ALL** instances)

![[Pasted image 20260922214002.png]]


# Armstrong's Axioms

- Inference rules to infer FD, applied repeatedly to infer all FDs

## Reflexivity:
If X is a subset of Y, then Y -> X
$\{Name\} \subseteq \{Name, Phone\}$ hence $\{Name, Phone\} -> \{Name\}$

## Augmentation:
If X -> Y, then XZ -> YZ for any Z
$\{ID\}$ -> $\{Name\}$, hence $\{ID, Phone\}$ -> $\{Name, Phone\}$


## Transitivity:
If X -> Y and Y -> Z, then X -> Z
$\{ID\}$ -> $\{Name\}$, and $\{Name\}$ -> $\{Phone\}$, hence $\{ID\}$ -> $\{Phone\}$

![[Pasted image 20260922214743.png]]

![[Pasted image 20260922214806.png]]


# Closure

- Given a set of FDs, how many new FDs can we **derive** ? How to find **all FDs** ?
	- Difficult to use inference rules in practice. Use **closure**

- Closure of X, denoted as $X^+$, where X is a set of attributes
	- $X^+$ is the complete set of **ALL possible attributes** that can be **functionally derived** from **given functional dependency** using the inference rules

## Closure Algorithm
- Input: Attribute of X, Set of FDs
- Output: $X^+$

1. Split FDs, each FD has a **single attribute** at the **right hand side**
2. While (changes to result) do
	1. For each B -> Y do
		1. If $B \subseteq Result$ then Result = Result

![[Pasted image 20260922215244.png]]

## Why Closure
- We can find ALL FDs easily
- Use closure to obtain all **super keys**
	- Start with X containing a **single** attribute
	- Stop as soon as **closure** contains **all attributes** in the relation schema
	- By varying starting attribute, you can obtain **ALL super key**

> [!Note]
> Closure allow us to answer 2 interesting questions
> - Is a particular dependency X -> Y **derivable** from F (FD) ?
> 	- Check whether **Y** in the **closure** of **X**
> - Are 2 sets of **dependencies** F and G **equivalent** ?
> 	- **Compare** their closures

![[Pasted image 20260922215732.png]]

![[Pasted image 20260922215751.png]]

![[Pasted image 20260922215759.png]]


# Normalization / Refinement
- FD whose **left hand side** is **NOT** a **super key**, hint a **redundancy**

> [!Definition]
> Process of designing a consistent database with minimum redundancy
> - If relation is in **normal form** certain kinds of problem can be avoided / minimized.
> - Normalization algorithms reduce the amount of redundancy by **decomposition**

## Normal Forms

- 1NF: All rows MUST contain the **same number of fields** (table is flat)
- 2NF: No partial key dependency (Old and obsolete)
- 3NF: No attributes dependent on non-key attributes
- BCNF: For most practical purposes, BCNF is acceptable
- 4NF & 5NF: Not covered and mostly not popular as well

![[Pasted image 20260922220218.png]]


## Boyce-Codd Normal Form (BCNF)
> A condition under which we can guarantee there is no anomalies


If and ONLY if for every of its dependencies X -> Y:
- X -> Y is a trivial FD (Trivial: Y is subset of X)
	- A -> A is trivial
	- AB -> A is trivial
- OR X is a superkey

![[Pasted image 20260922220421.png]]

![[Pasted image 20260922220433.png]]

# BCNF Algorithm

![[Pasted image 20260922220606.png]]

![[Pasted image 20260922220622.png]]

## Property of decomposition

> How do we know if a decomposition is correct or good ?

### Lossless Join
- Possible to **reconstruct** the **original** by a **natural join** on the decomposed schema
- If R is decomposed into S and T, ensure $S \cap T \neq \emptyset$ and $R = S \bowtie T$ (Natural Join)
- **Can** be achieved with BCNF

![[Pasted image 20260922221114.png]]

### Dependency Preservation
- Whether all the given FDs are **satisfied** after decomposition
- **May NOT** be achieved with BCNF


![[Pasted image 20260922221120.png]]

> [!Note]
> We can see here that the original FD is not kept

![[Pasted image 20260922221221.png]]

> [!Note]
> We can add JPC back into the table to make it dependency preserving BUT this will increase space required to store the whole database.


# Performance Considerations

> A database designer _may_ decide to use "bad" relations in a database because bad relations are often more efficient

![[Pasted image 20260922222730.png]]

- In this case if we need to query the table **frequently**, method 1 is better since all the data is already in 1 table and we don't have to spend time joining.































