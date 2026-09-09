---
title: W2 Requirements Engineering
tags:
  - Requirements
---
# Start of software development journey
- Figure out your stakeholders needs

### However
- Stakeholder may know what they want, but not necessary what is required.
- Stakeholders come from various domain expertise. Understanding the domain will significantly improve your understanding of their needs.
- As stakeholders understand their needs and project better, their requirements will naturally evolve

# "Moving Target" problem
- A change in requirements while software product is being developed
- Any change made to product can potentially cause a **regression fault**
	- A fault in an apparently unrelated part of the software
- If too many changes
	- Entire product may have to be redesigned and re-implemented

## How to solve it ?
- Pay attention and spend efforts at the requirement stage


# Software Requirements
#Requirements
- Description of service that a software system should provide and the constraints on its operation.
- Reflect the needs of stakeholders
- Requirements should be specific and quantifiable

## Challenges of Specifying Requirements
- Software is **intangible**, which makes it difficult to **comprehend** and **communicate**
- Stakeholders might not be clear about what they want.
- Terminology can be interpreted in multiple ways depending on the person or the context in which it is used.
- There are many **possible sources** of requirements
	- Direct users (end users) and indirect users (all other stakeholders)

## Understanding Requirements
![[Pasted image 20260905151145.png]]

## Levels of Requirements & Readers
![[Pasted image 20260905151215.png]]




# Activities of Requirements Engineering
1. **Elicitation**: Process of requirements discovery
2. **Analysis**: Refining and extending the initial requirements
3. **Validation**: Are we building the right product ?
4. **Management**: Needed because of the changing requirements


## Requirements Elicitation
> The starting point of every project

### What is a Stakeholder
- Any individual, group, or organization that has an interest in, is affected by, or can influence the development, operation, and success of a software system.

#### Examples of stakeholder
- If you are developing a mobile banking app:
	- End-users: Customers who use the app to transfer money
	- Client/Bank: Organization funding the app
	- Developers & Testers: Engineering team building it
	- IT Security Team: Ensures compliance with cybersecurity standards
	- Regulators: Financial authorities ensuring laws are followed
	- Customer service staff: Help customers if the app fails

#### Categories of Stakeholders
- **Primary** stakeholders (direct users & owners):  
	• End-users (who use the system daily)  
	• Product owners or clients (who request and fund the software)  
	• System administrators (who manage and maintain the system)  
▪ **Secondary** stakeholders (indirectly involved or affected):  
	• Managers (who rely on system reports or efficiency)  
	• Customer support teams (who assist users with issues)  
	• Marketing and sales (who sell or promote the product)  
▪ **External** stakeholders:  
	• Regulators or government agencies (who set compliance requirements)  
	• Investors (who fund the software development company)  
	• Competitors (indirectly influencing design/market decisions)  
▪ **Internal** stakeholders:  
	• Software developers and testers  
	• UX/UI designers  
	• Project managers  
	• Quality assurance teams

## Elicitation
> The process of requirements discovery

- It is different from requirements gathering
	- In elicitation, the focus in on **what user needs**, not just **wants**
	- Involves actively interacting with stakeholders to extract requirements
- Focus on **what** the stakeholder need, not **how** it will be done.
- The focus is on the problem, not the technical solution


## Requirements Discovery Methods
1. Interviews
2. Focus Group
3. Documents
4. Observations
5. Prototyping
6. Questionnaires
7. Scenarios

> IF O, DPQS
### Interviews
#### Purpose
- Capture stakeholders' needs, goals, pain points
- Clarify unclear or ambiguous requirements
- Explore both functional and non-functional requirements
#### Types of interviews
- **Structured**: Predefined questions, consistent format, easier to compare answers
- **Unstructured**: Open-ended, free discussion, more flexibility
- **Semi-Structured**: Mix of both, allows consistency with room for exploration
#### Preparation
- Identify relevant stakeholder 
- Prepare a question guide
- Set clear goals for what information is needed
#### Conducting the Interview
- Build rapport with the interviewee
- Start with general questions, then move to specifics
- Use **open-ended questions** to encourage detailed responses
- Use **closed-ended questions** to confirm facts
- Listen actively and avoid leading questions

#### Advantage
- Provides **deep insights** and context-specific information
- Allows clarification of vague requirements immediately
- Can uncover hidden needs and real pain points
- Builds trust and engagement with stakeholders

#### Disadvantage / Challenges
- **Time-consuming** if many stakeholders are involved
- Responses may be **biased** or **incomplete**
- Requires good interviewing skills to avoid **misinterpretation**
- Hard to cover **large groups** of users compared to surveys

### Focus Group
#### Purpose
- Gather requirements, opinions, and expectations from a **group of stakeholder** simultaneously.
- Stimulate discussion and generate ideas through **group interaction**
- Uncover conflicts, consensus, and priorities among different users
#### Structure
- Typically involves **6-12 participants**
- Led by facilitator / moderator who guides the discussion
- May use prompts such as scenarios, prototypes, or storyboards to trigger feedback
#### Preparation
- Carefully select **diverse but relevant** group of participants
- Prepare guiding questions/topics (Current pain points, desired features, usability concerns)
- Ensure a neutral and comfortable environment for open discussion.

#### Conducting the focus group
- Moderator introduces goals and sets ground rules
- Encourage participants to share experiences, needs, and suggestions
- Use open-ended prompts
- Record or document the discussion for later analysis
- Manage dominant voices and encourage quieter participants to share

#### Advantage
- Encourages brainstorming and creativity through group dynamics
- Can reveal share requirements and common pain points quickly
- Provides insights into conflicting priorities between stakeholders
- Faster than one-on-one interview for collecting diverse views
#### Disadvantage
- Risk of **groupthink** (Participants conforming to dominant opinions)
- Strong personalities **may overshadow** others
- Not ideal for sensitive or confidential requirements
- Requires a **skilled moderator** to keep the discussion productive

### Existing Documentation
#### Purpose
- Extract useful information about the system, processes, and constraints from already available documents
- Helps analysts understand the current system and business domain before engaging stakeholders
- Serves as a baseline for identifying gaps and improvements
#### Types of Documentation to Review
- Business Documents: Policies, Procedures, Contracts, Regulation
- System Documents: User manuals, Technical Specifications, Source Code Documentation
- Process Documentation: Workflow charts, SOPs 
- Historical Documents: Bug Report, Change Requests, Meeting minutes
- Standards & Compliance: Industry Regulation, Legal Requirements

#### Process
- Collect relevant documents from the client or organization
- Analyze for requirements-related information (Functional, non-functional, constraints)
- Highlight assumptions, ambiguities, or inconsistencies
- Validate findings with stakeholders (Documents may be outdated or inaccurate)

This is a sentence containing a <abbr title="This is your short note that shows on hover!">specific word</abbr> inside it.

#### Advantage
- Provide **objective**, **written evidence** (Less biased than personal opinions)
- Saves time, Reduces the need to "Start from scratch"
- Helps analyst prepare better for stakeholder interviews/focus groups
- Useful for understanding **regulatory and compliance requirements**
#### Disadvantage
- Documentation may be **outdated or incomplete**
- Risk of misinterpretation if the analyst is not familiar with the domain
- May not reflect real-world practices (Users often deviate from official processes)
- Still requires **validation** with stakeholders


### Observation
#### Purpose
- Directly watch stakeholder perform task in real work environment
- Identify requirements that may not be articulated during interviews or focus group
- Captures actual **workflow**, **pain points**, and **user behavior**
#### Types of Observation
- **Passive** Observation: Analyst observes silently without interfering
- **Active / Participant** Observation: Analyst interacts, asks clarifying questions, or even performs the task
- **Shadowing**: Following a user throughout their workday to see full workflow

#### Preparation
- Identify which processes, roles, or tasks to observe
- Get permission and explain the purpose to participants
- Prepare checklist or observation guides
#### Conducting the Observation
- Observe sequence of tasks, tools, interactions, and bottlenecks
- Take detailed notes, photos, or video recording (IF permitted)
- Minimize interference so users behave naturally
- Ask clarifying questions AFTER the activity (To avoid disrupting workflow)

#### Advantage
- Reveal **REAL practices**, not just what stakeholders say they do
- Identifies workarounds and hidden needs that may not appear in documentation
- Helps discover non-functional requirements
- Provides context for system integration with real-world workflows
#### Disadvantage
- Can be time-consuming, especially for complex processes
- Stakeholders may **alter their behavior** if they know they're being watched
- Some tasks may be sensitive 
- Observed data may need careful interpretation to avoid bias


### Prototyping
#### Purpose  
• To make requirements more tangible by creating a working model of the system.  
• To help stakeholders articulate requirements they may struggle to express verbally.  
• To validate assumptions early and reduce misunderstandings.  

#### Types of Prototypes  
• Throwaway (rapid) prototypes → quickly built to explore ideas, then discarded.  
• Evolutionary prototypes → incrementally refined until they evolve into the final system.  
• Low-fidelity prototypes → sketches, wireframes, mock-ups.  
• High-fidelity prototypes → interactive demos, partial system implementations.  

#### Process  
• Build an initial mock-up or simplified version of the system.  
• Show it to stakeholders and gather feedback.  
• Refine the prototype iteratively until requirements are clearer.  
• Use it as a communication tool between developers and stakeholders.

#### Advantages  
• Makes abstract requirements concrete and visual.  
• Helps uncover usability issues and hidden needs early.  
• Encourages active participation from stakeholders.  
• Reduces risk of delivering the wrong system.  

#### Disadvantages / Challenges  
• Can be time-consuming and costly if not managed properly.  
• Stakeholders may confuse prototype with the final product.  
• Risk of focusing too much on UI/visuals while ignoring deeper system  
requirements.  
• If used as throwaway, effort may feel “wasted” if not reused.


### Questionnaire
#### Purpose  
• To gather requirements, opinions, or preferences from a wide audience.  
• To collect both quantitative data (e.g., frequency of use, importance ratings) and qualitative data  
(e.g., open-ended feedback).  
• Useful for validating requirements across many users.  

#### Structure  
• Closed-ended questions → multiple choice, Likert scale (1–5 rating), yes/no.  
• Open-ended questions → free text responses to capture detailed opinions.  
• Often a mix of both for balance between measurability and insights.  

#### Preparation  
• Define clear objectives (e.g., “What features are most important to users?”).  
• Keep it concise (shorter surveys have higher response rates).  
• Pilot test the questionnaire before distribution.  
• Choose an appropriate delivery method (online form, email, printed survey)

#### Advantages  
• Can reach large numbers of stakeholders quickly and cheaply.  
• Provides quantifiable results that can be statistically analyzed.  
• Anonymity may encourage more honest responses.  
• Easy to compare responses across different user groups.  

#### Disadvantages / Challenges  
• Responses may lack depth compared to interviews or focus groups.  
• Poorly designed questions can lead to ambiguous or biased results.  
• Risk of low response rate, reducing representativeness.  
• No chance for immediate clarification (unlike interviews).


### Scenarios
#### Purpose  
• To describe realistic, story-like use situations of the system.  
• To help stakeholders visualize how the system will support their goals.  
• To uncover requirements related to workflows, exceptions, and edge cases.  
#### Structure  
• Actors (who is involved — users, systems, external entities).  
• Context (the situation or environment in which the scenario occurs).  
• Goals (what the actor is trying to achieve).  
• Steps/Interactions (sequence of actions between user and system).  
• Variations/Exceptions (what happens if things go wrong).

#### Advantages  
• Easy for stakeholders to relate to and validate (natural language, story-like).  
• Helps discover both functional and non-functional requirements.  
• Reveals exceptions and alternative flows that might be missed in interviews or  
questionnaires.  
• Provides a foundation for use cases, test cases, and prototyping.  
#### Disadvantages / Challenges  
• May oversimplify complex systems if not detailed enough.  
• Can be time-consuming to create comprehensive scenarios for all possible cases.  
• Risk of focusing too much on specific examples rather than general requirements.

## Blending Elicitation Techniques
> We blend techniques to be:
> - More effective with our engagement with the stakeholders
> - Speed up the requirements discovery

Often, requirements are not standalone. Blending techniques could bring up these types of requirements or relate one requirement to another.

# Analysis
- **Refining** and extending the initial requirements
- Extract more details that would help in **mapping** to a **solution**
- Could lead to many **modification** or the addition of new requirements

![[Pasted image 20260905164052.png]]


## 2 Major types of Requirements
> Functional Requirements "What"
> **Action / Tasks** that the software product must be able to perform from the **user** perspective

> Non-functional Requirements "How Well"
> **Quality Attributes** of the software product **Design Constraints**, such as Platform constraints and Response times

### Functional User Requirements
- Should describe the user requirements in **detail**
- Map problem to solution **without** implementation detail and in user's language
- Describe **interaction** between the system and its environment
- **Details** of requirement can highly affect your **planning and negotiation** with the client

> [!Detail can come from]
> - What does the system do ?
> - What are the alternative scenarios of success ?
> - What are the input/output ?
> - What happens when an error occurs ?

### Non-Functional Requirements
- How well will the system perform ?
- Quality Attributes
	- Reliability
	- Security
	- Usability
	- Performance
- Design Constraints
	- Platform Constraints
	- Response times
- Some are more important than the other for different industries
- Fill out the context of the overall Functional Requirements and determine overall quality

![[Pasted image 20260905164650.png]]

### Examples of Non-Functional Requirements
- Product Requirement  
The Patient Management System (PMS) shall be available to all clinics  
during normal working hours (Mon-Fri, 08:30-17:30). Downtime within  
the normal working hours shall not exceed five seconds in any one day.  

- Organisational Requirement  
Users of the PMS shall authenticate themselves using their health  
authority identity card.  

- External Requirement  
The PMS shall implement patient privacy provisions as set out in XXX

# What Makes a Requirement Good ?
1. Verifiable
	- Stated in such a way that it can be tested by inspection, analysis or demonstration
2. Clear & Concise
	- Must consist of a single requirement
	- Must be easily read and understood by nontechnical people
	- Not susceptible to multiple interpretations
3. Traceable
	- Has a unique identity or number
	- Cannot be separated or broken into smaller requirements
	- Can easily be traced through to specification, design and testing
4. Viable
	- Can be met using existing technology
	- Can be achieved within the budget
	- Can be met within the schedule
	- Does the organization have the necessary skills
5. Consistent
	- Does not conflict with other requirements
	- Uses the same terminology throughout the requirement specification
	- Does not duplicate other requirements or pieces of them
6. Implementation Free
	- Allows the system developer to decide what technology is best suited to achieve the function
7. Complete
	- Contains all the information that is needed to define the system function
	- Leaves no one guessing

# Prioritising Requirements
MoSCoW Prioritisation
- Categorise requirements into the following groups
	- Must-have
	- Should-have
	- Could-have
	- Will-not-have
- Give unique identifier to each requirement
- Identify tasks required to achieve each requirement
- Give unique identifier for each task and file them as an issue in your team's Kanban Board

# Requirement Specification can be represented in

## Natural Language Specification
- Requirements are written using numbered sentences in natural language
- Each sentence should express 1 requirement
- Supplemented by diagrams and tables

> 3.2 The system shall measure the blood sugar  
and deliver insulin, if required, every 10 minutes.  
(Changes in blood sugar are relatively slow so  
more frequent measurement is unnecessary; less  
frequent measurement could lead to  
unnecessarily high sugar levels.)

### Benefit 
Expressive, intuitive and universal. Requirements can be understood by users and customers

### Problems
- Lack clarity: Precision is difficult without making the document difficult to read
- Requirements confusion: Functional and non-functional requirements tend to be mixed-up
- Requirements mix: Several different requirements may be expressed together

## Structured Natural Language
- Requirements are written in a standard way.  
- Example of form-based specification:  
	• Definition of the function or entity.  
	• Description of inputs and where they come from.  
	• Description of outputs and where they go to.  
	• Information about the information needed for the  
	computation and other entities used.  
	• Description of the action to be taken.  
	• Pre and post conditions (if appropriate).  
	• The side effects (if any) of the function.


## Formal Specification
Requirement notations are written based on mathematical concepts such as finite-state machines or sets
![[Pasted image 20260905170410.png]]

### Advantages
- Unambiguous specifications, can reduce ambiguity in a requirements document
### Disadvantages
- Requires experts and takes more time
- Most customers don't understand a formal specification. They cannot check that it represents what they want and are reluctant to accept it as a system contract

## Graphical Notations Specifications
- Graphical models, supplemented by text annotations, are used to define the functional requirements for the system
- UML use case and sequence diagrams are commonly used


# Software Requirements Specification (SRS)

## Definition
A formal document that captures the complete description of a software system's requirements, including what the system should do and the constraints under which it must operate
## Purpose
- Serves as an agreement between stakeholders
- Provides clear, structured, and unambiguous reference for design, implementation, and testing
- Reduces misunderstandings and scope creep during development
## Characteristics of a Good SRS
- Correct: Reflect true stakeholder needs
- Unambiguous: Precise and clearly stated
- Complete: All necessary requirements covered
- Consistent: No conflict or contradictions
- Verifiable: Requirements can be tested
- Modifiable: Easy to update when requirements change
- Traceable: Each requirement can be tracked through design, implementation, and testing

# Validation
> "Are we building the RIGHT product ?"

- Validity: Does the system provide the functions that best support the needs ?
- Consistency: Are there any requirements conflicts ?
- Verifiability: Can the requirements be checked ?
- Realism: Can the requirements be implemented given available budget and technology
- Completeness: Are all functions required by the stakeholders included ?

## Validation Techniques
### Requirements Review & Walkthrough
Systematic manual analysis of the requirements

### Prototyping
Use an interactive / executable model of the system to check requirements

### Test-case Generation
Develop test cases for each requirement to check testability

# Management
> The process of managing changing requirements during the requirements engineering process and system development
![[Pasted image 20260905171400.png]]

















