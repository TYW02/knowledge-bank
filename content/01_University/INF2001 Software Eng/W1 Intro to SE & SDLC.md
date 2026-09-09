---
title: Intro to SE & SDLC
---
# Defining Software Engineering
> "The application of a systematic, disciplined, quantifiable approach to the development, operation and maintenance of software"

Software engineering is a discipline whose aim is the production of fault-free software, delivered on time and within budget, that satisfies the user's needs


## Fault-free Software
What are faults ?
- Software behaviours unaccounted for in its design

How can we lessen our changes of faults ?
- use a well-defined process that includes rigorous design, testing, and programming techniques

## Economic Aspect Example

If there is a new Coding Method that is 10% faster than currently used, should it be used ?
The common sense answer is: Of Course 

BUT Software Engineering answer:
- Consider the cost of training
- Consider the impact of introducing a new technology
- Consider the effect of new coding method on maintenance


## Satisfies User's Needs

### Functionality and Usability
- Does what the user's tasks require
- Efficient to use & error rates kept to a minimum 
- Easy to learn
- Leads to high user satisfaction

### Bad (even if correct) user interfaces cost
- Money (5% increase in satisfaction -> up to 85% increase in profits)
- Lives (Therac-25)

### User interfaces hard to get right


# Software development Activities
- Understand User Requirements (What the client needs)
- Analysis and design software architecture (high level and detailed)
- Implement and document the design
- Testing (Verify and Validate)
- Deploy the product
- Fix bugs after deployment
- Add features after deployment
- Planning and Team Management


## Typical Classical Phases

### Requirements Phase
- Explore the concept
- Elicit the client's requirements

### Analysis (Specification) Phase
- Analyse the client's requirements
- Draw up the **specification document**
- Draw up the software project **management plan**
- "What the product is supposed to do"

### Design Phase
- Architecture design
- Detailed design
- "How the product does it"

### Implementation and testing phase
- Coding
- Unit testing
- Integration
- Acceptance testing

### Postdelivery maintenance
- Corrective maintenance
- Perfective maintenance
- Adaptive maintenance

### Retirement


# Phase Cost Approximation
- Maintenance constitutes 67% of total cost
- Good software is maintained (for 10, 20 years or more)
- Bad software is discarded
- We should design our software with maintenance in mind.

> We need techniques, tools and practices to reduce maintenance costs


Software is a model of reality, which is constantly changing
Different types of maintenance
- **Corrective** maintenance (about 20%)
- Enhancement
	- **Perfective** maintenance (About 60%)
	- **Adaptive** maintenance (About 20%)


# Consequence of Relative Costs of Phases
- Reducing coding cost by 10% yields at most a 2% reduction in total costs
- Reducing postdelivery maintenance cost by 10% yields a 6-7% reduction in overall costs


# Requirements, Analysis and Design Aspects

To correct a fault **early** in the life cycle
- Usually just a document needs to be changed

To correct a fault **late** in the life cycle
- Change the code and the documentation
- Test the change itself
- Perform regression testing
- Reinstall the product on the client's computer

> To find faults as early as possible.
> To reduce the overall number of faults (and, hence, the overall cost)
> To reduce the cost of maintenance


# Software Life Cycle
A life cycle: The actual steps performed when building a product

A life cycle model:
- The steps to follow when building software
- A theoretical description of what should be done

Having a defined process (model) is essential
Maturity of the process is some gauge of success of organisation


## Waterfall Life-Cycle Mode

| 1.  | Requirements Phase             |
| --- | ------------------------------ |
| 2.  | Analysis (Specification) Phase |
| 3.  | Design Phase                   |
| 4.  | Implementation Phase           |
| 5.  | Postdelivery Maintenance       |
| 6.  | Retirement                     |
- **Sequential** & Distinct Phases: 1 phase is completed and the next one begins
- Document-driven (Plan and document approach)
- Big Design Up Front (BDUF)

### Waterfall feedback loop
The rationale is that the earlier you catch a bug the cheaper to fix it
However, it is not realistic
- Thus, you keep going back, then you must move forward again in sequence


### Attributes of the Waterfall Process

#### The Good
Waterfall model is easy to understand due to its simple linear structure and clearly defined stages.
Provides structure to less experienced staff
Facilitates project management
It helps to define the goal and deliverable at the early stage of the project

#### The Bad
Success depends on precise requirements
No working model of the software until the end of the life cycle
High amounts of risk / uncertainty
When in a later stage, it is very difficult to make any changes to the product
Not realistic: Does not reflect real processes
Expensive

### When to use Waterfall Model ?

#### When to use
Requirements are very well known and understood
Technology is understood
If you are building a new version of an existing product (with some exceptions)
Low-risk in-house projects
Small and simple projects
Government projects that are heavily regulated

#### When NOT to use
Not a great choice for complex and long-term project
Doesn't work for maintenance type project
When client is strict with timeline and budget
New idea that have not done before
Technology is new or team doesn't know it.


## Rapid Prototyping Model
- Linear model

### Instead of "Requirements"
- Listen to customer
- Build Prototype
- Customer "test drives" prototype
- Should be quick (can't be long)

### Challenges
- "Throw-away" phenomenon
- Demos can set unrealistic expectations
- Compromises that solidify


### Key points: Rapid Prototyping
DO NOT turn the prototype into product
Rapid prototyping may replace specification phase (Never the design phase)

### Comparison
Waterfall model (Try to get it right first time)
Rapid Prototype (Frequent changes, then discard)
But both methods only have 1 shot for delivery at the end

![[Pasted image 20260909200430.png]]
## Spiral Model
- 4 Specific phases
- Uses in iterations
- Combines planning and documentation with prototyping in iterations
- There is an emphasis on risk analysis
- The radius of the iteration reflects the accumulated cost involved
- Customer is involved throughout

![[Pasted image 20260909200556.png]]
### Attributes of Spiral Model

#### The Good
- Customers see the product as it evolves
- Risk management is part of the life-cycle (in every iteration)
- Project monitoring and scheduling are easy because of the clear phases
- Features can be added

#### The Bad
- Iterations are very long (0.5 - 2 years)
- A lot of documentation for every iteration
- You can't start a phase till the other ends
- Need staff who are experts in risk
- Identification and resolution
- Cost of the process is high (Time in prototyping)
- Requires Stakeholder engagement


### When to use Spiral Model ?

#### When to use
- High risk and large systems
- Can be used for totally new ideas

#### When NOT to use
- Client is not available
- Progress is urgent
- When client is strict with timeline and budget
- Low risk and low budget projects (Unnecessary expenses)


## Rational Unified Process
- Closely tied to UML and component-based modelling
- Unified Process is NOT a series of steps for constructing a software product
- Unified Process is an adaptable methodology
	- Must be modified for specific software product to be developed

### Phases of Business Context

#### Inception
- Begin to make initial business case
- Set tentative schedule and budget
- Risk assessment
- Understand the domain
- Usually short

#### Elaboration
- To refine the initial requirements and define priorities of use cases
- Refine the software architecture
- Refine the business case
- Refine the project management plan

#### Construction
- Emphasis is on implementation and Testing
- Integration testing of subsystems
- Product testing of overall system
- Operational releases
- Usually longer than the rest

#### Transition
- Move to customers' real environment
- Ensure that the requirements are met
- Correct Faults
- Complete Manuals
- Driven by feedback from client


### Key points for Rational Unified Process
- **Use case** and architecture centric
- Deals with software in **components** with defined interfaces
- Unified Process framework is an adaptable methodology

### Attributes of Rational Unified Process

#### The Good
- Business Process tied to development process
- Tool support for gradual improvement of a project
- Risk Mitigation
- Focus on quality of design
- A framework that allows the use of other models
- Doesn't need all requirements to be known at the beginning
- Deliver value early (if needed)

#### The Bad
- Complicated
- Expensive tools are needed
- Only good for medium and large-scale projects
- Extensive Documentation and planning (a lot of overhead)


### When to Use Rational Unified Process ?

#### When to use
- Medium to large projects
- Budget and schedule can be strict
- You need to show value early (Show something working in 1st iteration)
- Engineers experienced with Object-oriented design

#### When NOT to use
- Small simple projects
- Limited budget projects


## Agile 

The Agile manifesto has come to value:
- Individual & Interations
- Working Software
- Customer Collaboration
- Responding to Change

### Principles of Agile
- Embraces change as a fact of life
	- Continuous improvements over fixed phase
- Incremental delivery (1 - 4 weeks)
- Increments have value
- Emphasize Test driven development
- Small teams
- Customer involvement (not during iterations)
- The automation of tasks where possible
- Light-weight documentation
- Velocity is the way to measure progress (How to predict progress with past progress)
- Self management

### Types of Agile Methods
- XP Practices
- Scrum
- Kanban

### Practising Agile
- Gives the client confidence to know that a new version with additional functionality will arrive every 3 weeks
- The developers know that they will have 3 weeks (but no more) to deliver a new iteration
	- Without client interference of any kind
- If it is possible to complete the entire task in the timebox, the work may be reduced ("Descoped")
- Agile processes demand fixed time, not fixed features

### Attributes of the Agile method

#### The Good
- Flexible to change and continuous feedback which increases the chance of building the right product
- Customer Satisfaction
- Early value delivery and early to market
- Team Ownership (Self organizing team)

#### The Bad
- May require some rework (since we didn't know EVERYTHING upfront)
- Requires close collaboration with the client
- Good tools for automation are a must have (poor ones might delay you)
- Not every individual/team can adopt Agile values, setup needs trust and communication


### When to use Agile

#### When to Use
- Lightweight methods suit small to medium size projects (or large projects divided into components)
- Used for time-critical applications and prototypes
- Requirements are sure to change, new or uncertain
- Technology is new

#### When NOT to use
- Do not have a good team (Attitude and skills)
- For large projects where customer needs specific documentation and formal communication
- Large Systems that can't be broken into modules for smaller teams
















