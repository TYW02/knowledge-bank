---
title: W3 Use Case Diagram
tags:
  - UseCaseDiagram
---
# Use Case Diagram
- Describes how a **user** (actor) interacts with a system to achieve a **specific** goal
- Focuses on **functional requirements** (What the system should do)
- Captures the system's **intended behavior** in various scenarios

## Benefits of Use Case
- Bridge between **requirements** and **system design**
- Help stakeholders **understand system behavior** without technical details
- Provide a basis for:
	- System design
	- Test case development
	- Project planning

# Actor & Goal
- Actor: Anything with behavior (**Acts** on the software system)
	- Primary Actor: Initiates interaction to achieve goal
	- Supporting Actor: Performs **sub-goals** in use case
- Goal: The **desired outcome** an actor wants to achieve through interaction with the system
	- It expresses why the actor is using the system in the first place
	- Every use case should ultimately fulfill a goal
- Example: Customer withdraws money from an ATM machine
	- Actor: Customer
	- Goal: Withdraw money from ATM
	- Supporting Actor: The banking information database system (The ATM system queries it to retrieve the balance of the customer's account)


# Types of Goals

## User Goal (Primary Goal)
- **Main objectives** that actors want to accomplish
- **Directly** drive the creation of use cases
- Example: Book a flight ticket, borrow a book, purchase a product


## Sub-Goals (Supporting Goals)
- Steps **needed** to achieve a **larger goal**
- Often modeled as "include" use cases in UML
- Example: Authenticate User (supports Withdraw Cash)

### Examples of Goals in different domains
- ATM System: `Withdraw Money`, `Deposit Money`, `Check Balance`
- E-Commerce Site: `Search Product`, `Add to cart`, `Make payment`
- Library System: `Borrow Book`, `Return Book`, `Pay Fine`
- Learning Platform: `Upload Material`, `Enroll in Module`, `Take quiz`


# A Good Use Case

## Focuses on interaction
- Start with a **request** from an actor to the system
- Ends with the **production** of all the answers to the request
## Focuses on essential behaviours, from the actor's point of view
- Does not describe internal system activities
- Does not describe the GUI in detail
## Concise, clear, accessible to non-programmers
- Easy to read
- Summary fits on a page
- Main success scenario and extensions.


### Example Library Management System
- Functional Requirement
> "The system shall allow members to borrow and return books"

- Derived Use Cases:
	- Search book (Goal): Member (Actor) searches for a book
	- Borrow Book (Goal): Member (Actor) borrows a book (Includes Check Availability)
	- Return Book (Goal): Member (Actor) returns borrowed book
	- Renew Book (Goal): Member (Actor) extends borrowing period
	- Pay Fine (Goal) - Member (Actor) pays overdue fines

# Use case vs Internal Features
> Consider software to run on a cell phone

## Use Case
- Call someone
- Receive a call
- Send a message
- Memorize a number
> Point of View: User
## Internal Functions
- Transmit / receive data
- Energy (Battery)
- User I/O
- Phone-book Management
> Point of view: Developer / Designer


# Presenting Use cases
1. Summary of Use Cases
	- Methods 
		- Actor/Goal List
		- UML Use Case Diagram
2. Writing each Use Case

![[Pasted image 20260912175127.png]]

![[Pasted image 20260912175145.png]]

![[Pasted image 20260912175202.png]]

# Use Case Diagram: Actors
- An actor is a member of the **world outside** the software product
- An actor is **frequently** a user of the software product
- In general, an actor **plays a role** with regard to the software product.
	- **User**
	- **Initiator**
	- Someone who plays a **critical part** in the use case

> [!NOTE]
> Name actors base on the function it plays

## More on Actors
- An Actor need not be a human being

### Example
> An e-commerce information system has to interact with the credit card company information system
- The **credit card company information system** is an **Actor** from the viewpoint of the e-commerce information system
- The **e-commerce information system** is an **Actor** from the viewpoint of the credit card company information system

![[Pasted image 20260912175719.png]]


# Use Case Diagram Stereotypes \<include\>

```
<<include>> defines a mandatory relationship where a base use case explicitly integrates the behavior of another use case
```

![[Pasted image 20260912180206.png]]

- Check balance **includes** Validate Pin use case
- Validation Pin process is **required** in Check Balance (not optional)
- Validate Pin use case is **extracted** for reusability since other use cases use it.
- Validate Pin is **not created** to stand on its own as a use case

## How to Use Stereotypes \<include\>
- "Validation Pin" use case is **required** in the "Check Balance" use case. This means that **whenever** "Check Balance" use case occurs, the **entire** "Validation Pin" use case **must always take place**.
- It usually only make economical sense to use \<include\> when the included use case is **required by more than 1 use case**.
- "Check Balance" & "Withdraw Cash" use cases **required** "Validation Pin" use case.

# Use Case Diagram \<extend\>
> Defines an optional relationship where an extending use case inserts its behavior into a base use case only under **SPECIFIC** conditions


![[Pasted image 20260912185205.png]]

- "Report Forgery" extends "Validate ID Card" to add to its functionality
- **Optional** use case that usually depends on a set of conditions in the validate ID card use case
- NOTE: Arrow Direction

# Writing a Use Case Description
- Detailed description of the user's interaction with the software product to achieve a goal
- Describe what will happen in all possible scenarios

## Use Case Description Template
- Use Case ID: Unique Identifier
- Use Case Name: Action name
- Description: Quick overview
- Primary Actor: Entity that acts on the system or another system
- Pre-conditions: Indicates what the system will ensure is true before letting the use case start
- Main success scenario: Steps needed for the user to achieve the main goal
- Alternative Scenario: Describe all the other scenarios for this use case (Including exception)
- Post-Condition: Indicate what system will ensure is true after the use case is done (Can be specific to different scenarios)
- Priority: Low, Medium, High
- Non-Functional Requirements (if any): Any specific non-functional dependencies ?


![[Pasted image 20260912185654.png]]

![[Pasted image 20260912185700.png]]

## Main & Alternative Scenarios
![[Pasted image 20260912185729.png]]

## Example of Use Case Description
![[Pasted image 20260912185746.png]]


# Activity Diagram
> Describe the workflow behavior of a system

- Used in process modeling and analysis during requirements engineering
- Most useful for understanding workflow analysis of synchronous behaviors across a **process**

> [!Main Reason]
> Model the workflow behind the system being designed.
> - Documenting existing process
> - Analyzing new Process Concepts
> - Finding re-engineering Opportunities

![[Pasted image 20260912190013.png]]


# Components of Activity Diagram
![[Pasted image 20260912190038.png]]

![[Pasted image 20260912190045.png]]

![[Pasted image 20260912190052.png]]

## Example of Activity Diagram
![[Pasted image 20260912190107.png]]


## Activity Diagram Concepts
- Activity is triggered by 1 or more events and activity may result in 1 or more events that may trigger other activity or processes.
- Events start from **start symbol** and end with **finish marker** having activities in between connected by events

- Activity Diagram represents decisions, iterations, parallel/random behavior of the processing
	- Capture actions performed
	- Stress on work performed in operations (Methods)

## Disadvantages
> DO NOT explicitly present which objects execute which activities, and the way that the messaging works between them.

- Labeling each activity with the responsible object can be done
- Useful to draw activity diagram early in the modeling of a process, to help understand the overall process.













