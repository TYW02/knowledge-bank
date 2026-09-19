---
title: W4 Class Diagram & Sequence Diagram
tags:
  - Class_Diagram
  - Sequence_Diagram
---
# Benefits of Object-Oriented Paradigm
- Increase **REUSE** due to modularity
- Increase **maintainability** since it accommodates for changes while protecting the existing structure
- Help enforcing good design techniques
- Real-world like design makes it more understandable by non-technical audience


# Object-Oriented Analysis and Design
- Classes & Objects
- Noun Extraction
- Modelling
- Class Diagram
- Class types
- Sequence Diagram

## Class & Object
- A program template to define the data (Attributes) maintained by the object and services/operations/behaviours performed by it

![[Pasted image 20260919175324.png]]

![[Pasted image 20260919175355.png]]

![[Pasted image 20260919175404.png]]

![[Pasted image 20260919175411.png]]

![[Pasted image 20260919175417.png]]


# From Use Cases to Classes

## Entity Classes
> Entity definition
> - A thing with distinct and independent existence

> Entity Classes
> - Long-lived, data-bearing business objects of the system


### Use Case -> Class: 4 Steps
1. Write a **Solution Abstract** for Use Cases
	- A high-level conceptual text, system narrative, or domain-level synthesis of how the use case will be solved technically
2. Filter the raw list of **Nouns** to extract **Entity Classes**
	- Person, place, thing, animal or idea
3. Determine **Attributes** & **Services** of Classes
4. Derive **Relationships**

#### Example
![[Pasted image 20260919175749.png]]

![[Pasted image 20260919175816.png]]

![[Pasted image 20260919175902.png]]

![[Pasted image 20260919175927.png]]

![[Pasted image 20260919175942.png]]



# Object-Oriented Design Concepts

## Inheritance
> Enables **re-use** of higher level class specifications among more detailed implementations

- The sub-class **inherits the properties** and behaviours of the super class

### Use INHERITANCE to Reuse Objects
- In inheritance, the sub-class **inherits** the **properties** and **behaviours** of the super-class
- Sometimes it is very clear if you find the "is a" relationship among entities
- Duck "is a" Animal


## Polymorphism
> Enables **multiple implementations** to handle the **same** message from a client in different ways, in a manner which is **transparent** to the client.


## Encapsulation
- Grouping of **data** and **functions** into a component
- Selective hiding of **attributes** and **operations**

### Information Hiding & Encapsulation

Apply the same concepts for everything
- Method
- Class
- Module / Component
- A whole application

### How to use Encapsulation & Information Hiding

##### No Direct Access
> Encapsulation and information hiding of the state and internal behaviour of an object so that is not directly accessible to external service clients

##### Internal states are regulated
> Access to internal state can be regulated by the specification of an object's operations. 
> 
> Operations can be provided to **create** a new instance (A Constructor), **alter** an object's **state** (A Mutator) or **access** the **state** (An Accessor)

##### Services
> System development is concentrated on what the services an object provides can do, **NOT HOW** it does it.



## Member Visibility
![[Pasted image 20260919180930.png]]

![[Pasted image 20260919180943.png]]

![[Pasted image 20260919181011.png]]


# How about interactions among objects ?

> [!Problem]
> - Buttons do not communicate **DIRECTLY** with elevators
> - We need an additional class: **Elevator Controller**

![[Pasted image 20260919181133.png]]


# Sequence Diagram
> Interaction Diagram that models a single scenario executing in the system

- Visualize interactions over time
- Clarify system behavior
- Bridge between requirements and design
- Identify responsibilities and collaboration
- Facilitate communication

## Key Parts of a Sequence Diagram
- **Participant**: An object or entity that acts in the sequence diagram
	- Sequence diagram starts with an unattached "Found message" arrow
- **Message**: Communication between participant objects
- The **axes** in a sequence diagram
	- **Horizontal**: Which object / participant is acting
	- **Vertical**: Time (Down -> Forward in time)

![[Pasted image 20260919181949.png]]

# Representing Objects
- Squares with object type, optionally preceded by object name and colon
- Write object's name if it clarifies the diagram
- Object's "life line" represented by dashed vertical line
![[Pasted image 20260919182101.png]]

## Messages between objects
- Message (Method Call) indicated by horizontal arrow to other objects
	- Write message name and arguments above arrow
	- Dashed arrow back indicates return
	- Different arrowheads for normal / concurrent (Asynchronous) methods
![[Pasted image 20260919182150.png]]

![[Pasted image 20260919182236.png]]

# Lifetime of objects
- **Creation**: Arrow with "new" written above it
	- Notice that an object created after the start of the scenario appears lower than the others
- **Deletion**: An X at bottom of object's lifeline
	- Java doesn't explicitly delete objects, they fall out of scope and are garbage-collected

![[Pasted image 20260919182445.png]]

# Indicating Method Calls
- **Activation**: Thick box over object's lifeline, drawn when object's method is on the stack
	- Either that object is running its code, or it is on the stack waiting for another object's method to finish
	- Nest to indicate recursion

![[Pasted image 20260919182624.png]]


# Indicating Selection & Loops
- **Frame**: Box around part of a sequence diagram to indicate selection or loop
	- `if` -> (opt) \[condition]
	- `if/else` -> (alt) \[condition], separated by horizontal dashed line
	- `loop` -> (loop) \[condition or items to loop over]

![[Pasted image 20260919182819.png]]


## Linking Sequence Diagrams
- If one sequence diagram is **too large** or **refers** to another diagram, indicate it with either:
	- An **unfinished arrow** and comment
	- A "ref" frame that **names** the other diagram
	- When would this occur in our system ?

![[Pasted image 20260919182943.png]]

# Why not just code it ?

Sequence diagrams can be **somewhat close** to the code level. So why not just code it up rather than drawing it as a sequence diagram ?
- A good sequence diagram is still **a bit above** the level of real code (Not all code is drawn on diagram)
- Sequence diagrams are **language-agnostic** (Can be implemented in many different languages)
- Non-coders can do sequence diagrams
- Easier to do sequence diagrams as a team
- Can see many objects / classes at a time on same page (Visual bandwidth)





















