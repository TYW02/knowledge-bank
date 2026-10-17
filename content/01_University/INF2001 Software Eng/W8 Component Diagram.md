---
title: W8 Component Diagram
---
A Component Diagram is a Structural Diagram

# What are Software Components ?

Components are **independent unit** within a system that **encapsulates a collection of data** and **functions** that are semantically **related**.

- Components are **higher-level abstractions** than **objects** and **encapsulate** (hides) their **internal structure**
- Components **collaborate** with other components through **well-defined interfaces**
- Component can be collection of classes, Web service, resource

> [!Info] Design Criteria
> Components should be 
> - Modular
> - Portable
> - Replaceable
> - Reusable

## Benefits
- Make discussion easier at a higher-level. Especially with clients

# Component Diagram Notation
![[Pasted image 20261017190156.png]]


# Component Providing Interface Notation
![[Pasted image 20261017190224.png]]

![[Pasted image 20261017190242.png]]

# Nested Components
![[Pasted image 20261017190257.png]]


# Ports and Delegates
![[Pasted image 20261017190346.png]]

![[Pasted image 20261017190430.png]]

> [!warning] Why use Port and Delegate
> To model **how** components **interact** with **other (external) components** and how the **responsibility** for realizing **external requests** are delegated throughout parts of the components


![[Pasted image 20261017190601.png]]


# Component Diagram at a Glance

> [!info] What does a Component Diagram actually do ?
> It **breaks down** the actual system under development into **various high level functionality**.
> - Each component is responsible for **1 clear aim** within the entire system and **only interacts** with other essential elements on a **need-to-know basis**.
> 


![[Pasted image 20261017190810.png]]


# Components Possibilities

**Any** encapsulated unit in the system **can be a component**

> [!failure] REMEMBER
> Components **encapsulate** their **internal structure**, therefore, **collaboration** with other components is achieved through **well-defined interfaces**.
> 

![[Pasted image 20261017191104.png]]


# Common Mistakes

> [!warning] Components are higher level abstractions that objects and encapsulates internal structure
> DO NOT provide too much detail

- There should **not** be any "**dangling**" lollipop or socket that does not have a **corresponding connection** (UNLESS its to external component)
- **DO NOT share lines** in notation

> [!warning] When to use port
> When you want to represent a specific point of interaction provided by an encapsulated component

- Double check modelling especially when a **component only has required** but NO provide or vice versa. (Could be wrong interface or something missing)
- User interface **DO NOT need** to be a separate component
- Component can have **both required** interface and **provided** interface
- Ball can be shared by more than 1 component









































