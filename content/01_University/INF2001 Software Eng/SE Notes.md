# **Components** 
* **Independent unit** in system that **encapsulate collection of data and function** that are semantically related  
* **Higher-level** abstraction than **objects**, hides their internal structure  
* **Collaborate** with other component through **interfaces**  
* Can be collection of **classes** (package), **Web Services**, **Resource**  
* Design Components to be **modular**, **portable**, **replaceable**, **reusable**  
* A provides interface for others to collaborate (Can define exactly how it accepts Collaboration)

Port \[Access Point to external environment access\]

![[Pasted image 20261119235225.png]]
### **Checklist**

* Should have matching / paired Socket or lollipop  
* Don't share line  
* UI / Dashboard do not need Separate component   
* Lollipop can be shared by more than 1 component  
* Usually an exposed interface matches to one interface class in the class diagram

**Software Engineering Design** 

* Process of identifying, evaluating, validating, Specifying Architectural Detailed Construction models required to build software 

**Product Development Perspective** 

* Reuse Solution in other project   
* Design forms foundation for all development activities   
* Identify component & interface   
* Provide means to evaluate quality attribute   
* Requirements are mapped to conceptual model of Software 

**Project Management** 

* Minimize effects of requirement volatility   
* Design decompose System to work in parallel and distribute work  
* Multiple people own multiple component   
* Design help improve project management, planning, organization, Staffing, tracking 

**Software Design process**:  
Activities & controls that specify how resources work together 

**Software Architecture**: 

* Macro design to model and quality & function of Software system   
* Black box model to evaluate system projected capabilities and lay foundation for ALL Subsequent work,   
* Focus on **Non-Functional Requirement** 

**Detailed Design**: 

* Builds on software architecture to provide white-box design elements  
*  **Refine Software architecture** where Software design, architecture & detailed design are Sufficiently complete for **Construction to begin** 

**Construction Design**: Support System quality attribute, Performance, maintainability, testability   
**Human-Computer Interface**: Optimize Interface between human and computer 

**Software Design Management**: Activities required to create & implement quality design artifacts **within schedule** and budget constraints. 

# **Software Design Fundamentals** 

**Modularization** : Continuous decomposition until fine-gramed components are created. 

Can be achieved through Abstraction & Encapsulation 

**Cohesion**: Degree which all elements work together as a functional unit 

(High cohesion is good, Low cohesion is bad) 

**Coupling**: Degree of interdependence between 2 or more components 

(Tight coupling is bad, Loose coupling is good)   
**Separation of Interface (Visible) & implementation (Hidden)**

Define component by specifying public interface that is separate from details of how component is realized. 

### **Completeness & Sufficiency** 

**Completeness**: measures how well designed units provide the required Services to achieve the intent (**NO LESS**) 

**Sufficiency**: How well designed units are at providing only the service that are sufficient for achieving the intent (**NO MORE**)   
**Software Architecture**: Stakeholders' concern serve as driving force behind architectural decision 

**When deciding architecture**: 

* Functional & Non-Functional dictate what we do   
* Manage trade-offs   
* Adhere to Software Quality Requirements 

### **Software Quality Requirement** 

* **Usability** → Complexity when learning / using system   
* **Maintainability** → Complexity in fixing any issues or making changes to System   
* **Security** → Ability to protect/ defend system   
* **Performance** → Capacity to accomplish useful work under resource constraints   
* **Reliability** → system failure rate   
* **Portability** → complexity when adapting system to other software / hardware environment   
* **Testability** → complexity when verifying and validating system function   
* **Availability** → Degree to which system or component is operational & accessible   
* **Interoperability** → System ability to collaborate with other software / hardware Systems 

**C4 Model**: Context, Container, Component, Code   
\[Good architecture diagram clearly communicates what it needs to do, who it needs to communicate to\]  
**Container**: Containers are **runnable** or **deployable** parts inside the system

4 + 1 Model:   
Follows **UML diagrams**  
**Logic View**: Logical class, State, component diagram (Functionality of system)  
**Development view**: Package diagram, source code, systems from programmer’s POV  
**Process View**: Sequence communication, Activity diagram (How system process / communicate)  
**Physical View**: Deployment diagram (Topology of software on physical layer)  
**User View** (Scenario view) (Show how the 4 view work together)

### **Key Task in Architectural Design.** 

**Identify:** 

* Stakeholder concern   
* Architectural view   
* Architectural style & Pattern   
* Influence of architectural decision in organisation   
* System's major component & interface 

Evaluate & validate: Architecture 

Establish policies for ensuring architectural design synchronicity

### **Pattems: Solution to recurring problem** 

**Architectural Pattern classification: (Give fundamental structural organisation)**

**Data-Centered :** Centralized repository for data, allow client to access & work on data 

**Data flow**: Transport & transformation of a stream of data 

**Distributed**: Interaction between several independent processing unit connected via network, (Layered Pattern: Each layer performs a specific role. Component/classes organized into horizontal layers )

**Interactive**: System that serve users or user-centric Systems 

**Hierarchical**: components structured as a hierarchy to reflect different level of abstraction (Client-Server Pattern)

### **Layered Pattern Hierarchical** 

**Presentation Layer**: Focus on user interface concerns (Devoid of business logic)

**Business / Application Layer**: Implementation of business logic validation calculation logic 

**Data Layer**: Functionality to access and manage data (provide service & data for business) 

* Each layer is a level of abstraction around a role   
* Each layer NOT concerned with the "how" of the other layers   
* As request move from layer to layer it MUST go through the layer below it 

**Layers of isolation**: Changes made in one layer does NOT impart or affect other layers **Disadvantage** 

* More Code   
* Have to be diligent about placing code in correct layer to NOT leak logic   
* In efficient for request to go through multiple layers 

### **Distributed** 

**Client-Server pattern** 
![[Pasted image 20261119235310.png]]

**Interactive** 

**Model-View-Controller (MVC):** 

Widely used in interactive application, flexible human-computer interface 
3 component to handle: System's input, processing, output   
![[Pasted image 20261119235333.png]]

**Design Patterns (Help implementation of smaller subsystems)**

**Creational**: Creating Objects 

**Structural:** Managing relationship between objects 

**Behavioral**: Implementing common behavior 

### **Factory : Creational** 

Responsible for instantiating other classes 

**Intent**: provide method which object can be created, subclass to decide which concrete class to use 

**Applicability:** 

* Concrete type determined at run-time   
* More concrete type added over time   
* Encapsulate logic of choosing concrete type in single function 

![[Pasted image 20261119235351.png]]

**Singleton: Creational** 

* Has a private constructor  
* Private attribute that holds the single instance  
* Public GetInstance() that returns the instance

**Intent**: Ensure only **1 instance** of class exists 

**Applicability**: Provide access to unique resources, grouping global variables 

**Observer: Behavioural** 

Generates a list of events/ maintains a list of observers (or listeners) that will be 

notified when an event arrives 

**Composite: Structural** 

Re-use existing classes in new context and build complex structure from simpler Components 

**Non-executing based testing**: Walk through, Inspection 

* Check for quality without running test case   
* We should NOT review our own work

Walk through (Detect faults, NOT correct them) 

* Static analysis techniques   
* Designer / Programmer leads parties through Software product & participants ask questions and make comments about error, violation of standards and other problems 

**Major Objectives**: 

* Find anomalies   
* Improve Software product   
* Consider alteratives   
* Evaluate conformance to standards & specification 

### **Inspection** 

Systematic examination 

**Verify Software product (Are we building the system right to spec)**

* Satisfy Specification   
* Satisfy Specified quality attribute   
* Conforms to applicable regulation, Standards, guidelines, Plans, procedures Identify deviation from Standards & Specification 

**Metrics** 

* Inspection rate   
* Fault density   
* Fault detection rate   
* Fault detection efficiency 

| Walkthrough | Inspection |
| :---- | :---- |
| 2 Step, informal process  | 5 Step, Formal process  |
| Preparation  | Overview  |
| Analysis  | Preparation  |
|  | Inspection  |
|  | Rework  |
|  | Follow-up  |

**Execution Based testing** 

* Testing via running code   
* No False Positives (Directly observes actual behaviour of code *under* test)   
* Can be automated 

**Tests** 

* Correctness \[correct if satisfies specification, Spec may be incorrect or correct but incomplete\]   
* Utility \[If product meets user needs, Ease of use, useful function\]   
* Reliability \[measure of frequency & criticality of failure\]   
* Robustness \[ Range of operating condition, Effect of invalid input\]   
* Performance \[Extent to which spare & time constraints are net\] 

| Blackbox | Whitebox |
| :---- | :---- |
| Functional, Behavioural Testing Test observable functionality of application | Transparent Testing Test based on internal structure or workings of application |

### **Black box testing** 

* Conform to **specification** / **Derived from specification**   
* Input to System and compare output against pre-defined test Spec 

(Given input, DO NOT care How output is produced, only whether output is desired and expected) 

* Test Can be functional or non functional 

| Applies at Unit, Integration, System and Acceptance Levels Designing test requires NO knowledge of underlying system  Does Not require programming Skill |
| :------------------------------------------------------------------------------------------------------------------------------------------------------- |

(Different technique different guarantees and assurance)

### **Equivalence Partitioning (Blackbox technique)**

Relies on **system requirements** and **input domain specification** without inspecting internal source code.

Divide input values into valid and invalid partitions, select values from each partition as test data 

Example: Accept value between 50-90% 

| Invalid | Valid | Invalid |
| :---- | :---- | :---- |
| \< 50 | 50 \- 90 | \> 90 |

To test: 

* Choose 30 from Invalid Partition 1 → Reject   
* 60 from valid partition → Accept   
* 100 from Invalid Partition 2 → Reject 

(Come up with as few partition as possible) 

(Randomly choose test values within partition)

### **Boundary Value Analysis** 

**Test values at boundary** (More error occur at boundaries) 

Choose values **AT & NEAR** boundaries 

To test: choose 49   
Reject 

| 49 | Reject |
| :---- | :---- |
| 50 | Accept |
| 51 | Accept |
| 89 | Accept |
| 90 | Accept |
| 91 | Reject |

### **Decision Table** 

Cover ALL combination of input (conses) and output (Effect) 

1. List all causes    
2. Calculate Possible combination   
3. Fill columns with possible combination   
4. Add effect to table   
5. Reduce test combination   
6. Check covered combination 

![[Pasted image 20261119235525.png]]

Once reduced, come up with Specific test case to pass to Tester 

**NOT Suitable** for System with large number of causes 

### **White box testing** 

\[Blackbox cannot reveal errors due to implementation details\] 

\[whitebox cannot reveal errors due to missing paths\] 

**Goal**: 

* Uncover bugs in a small but carefully selected subset of input domain   
* Process every single character in code and test for errors 

**Unit testing**: Individual Modules 

**Integration testing**: Test between units, interaction among modules 

**Regression testing**: Performed every time we change our system 

### **Coverage Criteria** 

* Standards used to measure how thoroughly code has been tested   
* Systematic way to test cases, Help find gaps in testing & improve software reliability   
* 100% coverage does not guarantee absence of bugs BUT increases confidence in Code's correctness 

### **Statement Coverage** 

**Test Requirements**: Statement in the program   
**Coverage Measure**: (lines of code covered by tests / total lines of code) ×100 

**Process**: Highlight each line of code that is actually fun based on Test-case 

\[Focus on verifying whether each statement in code executes at least once\] 

\[ Does NOT guarantee ALL possible execution paths, Does NOT test different Combinations of conditions that might influence program flow\] 

**Control-Flow Graph**   
Help visualize statement & control in module   
**Statement**: Nodes 

**Flow of control**: Edges 

Node with more than 1 outgoing edge \= Branch 

**Path**: Route we take with code from start to finish   
![[Pasted image 20261119235545.png]]

1. void Truth loop ( int greatness) {  
2. for (int i=0; i\< 10; i++) {   
3. if (greatness \>10){   
4. Print(" ")}}   
5. else  
6. print(" ")   
7. }

(Same number of Nodes as line of code) 

Cyclomatic Complexity (M): Used to indicate complexity of program 

Upper bound for number of path in set of basis path 

**Number of linearly independent paths** M \= E-N+2P   
8-7+2(1)=3 

**Branch coverage**:   
Attempts to explore all Possible branch 

Statement testing may not reveal all possible paths that code may take hence, may not show all necessary test we should run 

**Branch Coverage** (%) \= (Number of branch executed & tested / Total number of branches)

**Test Requirements**: Branch in program   
**Path Coverage**: Generate coverage such that all paths in the program are covered \[very expensive, non-trivial program may have virtually infinite number of paths\] 

### **Control Flow Testing** 

* Test all possible independent paths in control flow graph   
* Best executed for procedures   
* **Guarantee**: Every Statement of Program been executed at least once and every transition was tested   
* **Helps**: Figure out how many test cases are needed, How to construct each test (what to test)   
* **Basis Paths**: Set of path that any other path can be "constructed "out of combination of basis paths Include all edges of the graph\]   
* Tested all possible paths at least once linearly independent) 

**Determine set of basis path** 

1. Pick baseline that corresponds to normal execution \[Aim for many decision as possible\]   
2. For Succeeding basis paths, back track baseline until decision node. "Flip" decision and continue as much of baseline as possible   
3. Repeat until all decision have been flipped. When you reach M basis path. 

![[Pasted image 20261119235600.png]]
### **Coverage Type** 

| Coverage Type | What it requires | What it ensures |
| :---- | :---- | :---- |
| Statement  | Execute every Statement at least once | Codeline tested  |
| Branch  | Execute each branch of every decision | Decision logic tested  |
| Path  | Execute all possible path through the code  | Full logic combination  tested  |

Statement Coverage → Did we run every line 

Branch coverage → Did we test True & False outcome 

Path coverage → Did we test all possible way the program can execute 

### **User Acceptance Testing** 

* UAT is not system testing   
* Not looking for major error, hopefully no error 

**System testing** 

* Software does not crash, meet documented requirement   
* Accept correct input & give correct output   
* Important segment has been tested   
* Resource consumption & load time 

### **Application Packaging** 

Develop final deliverable: 

* Ensure consistent, Stable & reliable standard environment   
* Increase efficiency of software management   
* Mitigate security issues   
* Decrease risk for business disruption   
* Help reduce on-gong administration & Support cost 

\[Document installation, Prerequisite included, Auto-installer, Supporting document, Licensing agreement\] 

**Refactoring** \[**NOT** adding features, Debugging code, Rewriting code\] 

* Restructuring Code   
* Small, Sematic-preserving transformation   
* Make the code easier to maintain and modify 

Changes **internal structure** without changing **observable behaviour**

Can still affect **non-functional properties** such as speed or security

“Bad Smell" Code Pattern   
**Cloning (Duplicate code)** 

* Complex Structure   
* Long method   
* Large classes 

**Variable & Parameter** 

* Long parameter list   
* Feature envy   
* Data dumps   
* Primitive obsession   
* Temporary field 

**Control structure & Polymorphism** 

* Switch statement   
* Refused bequest   
* Alternative classes with different interfaces 

### **Cloning** 

**Causes** 

* Multiple Programmers \[Colleague already written Similar code\]   
* Purposeful duplication \[Rushing to meet deadline with copy & paste\] 

**Why bad?** 

If you find bug in original, you have to fix all clones as well 

**Refactoring Technique**: Extract method 

* Create new method that encapsulate duplicated code   
* Replace code clone with method call 

### **Large class** 

**Causes** : Small class can get bloated as program grows 

**Why bad?** 

Class may become non-realistic model, May have responsibility confusion 

**Refactoring technique**: Extract class 

* Create a new class   
* Move field & method responsible for relevant functionality into new class 

### **Feature Envy** 

**Causes**: Indication of method that was incorrectly placed in the wrong class 

**Why bad?** 

Indicate abstraction fault or may indicate the method was incorrectly placed in wrong class 

**Refactoring technique**: Move method 

Move method with feature envy to class containing most frequently used methods & data items 

### **Switch Statement** 

**Causes**: case in switch statement contain logic for different type of instance of the same class 

In OOP, this indicate new subclass should be created 

**Why bad?** 

Same Switch/case structure appear in many places 

**Refactoring technique**: Extract subclass & Extract Method 

* Create new Subclass   
* Extract method to move case block logic into methods on new Subclass   
* Use polymorphism to Substitute the switch block 

### **Limits of refactoring Change can affect** 

*  Non-functional properties   
* The API of a system 

**Refactoring that alter APIs happen when** 

* Class member is moved   
* Class member is renamed   
* List of parameter to operation is changed 

### **Adaptive Maintenance**

Modifying existing software or systems so they stay **compatible**, **compliant** and **functional** when their **external environment** or **requirements change**.

### **Corrective Maintenance**

Corrective repairs faults

### **Perfective Maintenance**

Perfective enhances functionality, usability or performance for users

### **Preventive Maintenance**

Preventive heads off future problems such as missing validation, the trigger here is external  
Prevent problems BEFORE they occur

### **Variants**

Functionally **equivalent** versions designed for **different settings** such as **hardware** or **software**.

### **Change Control Board (CCB)**

**Body** that **approves or rejects** a change request **AFTER** the **impact analysis**

### **Version Management**

Keeps track of versions of configuration items and prevents interference

### **Release Management**

Prepares and tracks external releases

### **System Building**

System building assembles and compiles the system

### **Change Control**

Change control tracks requests, works out cost and impact, and decides on changes



