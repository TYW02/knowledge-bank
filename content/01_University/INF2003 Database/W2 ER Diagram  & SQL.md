---
title: W2 ER Diagram & SQL
tags:
  - ERDiagram
  - SQL
---
# ER Diagram
Consists of:
- Collection of **Entity**
- Collection of **Relationship**
- **Attributes** associated with entity and relationship sets
- **Connections** between entity and relationship

## Symbols used in lecture

**Entity**: Rectangle
- Lines to its attributes and relationships
- Underline the **Primary Key**
**Relationship**: Diamond
**Attribute**: Oval / Ellipse
- Double Ellipse: Multivalued Attribute
- Dashed Ellipse: Derived Attribute

![[Pasted image 20260908202933.png]]

# ER Model - Entity

> A unique object in real-world
- Each entity has a set of attribute
- Each attribute has a data type
- A subset of the attribute can uniquely identify the entity

## Entity Set

^e62f72

> A collection of entities, with the same properties
- Same attributes, same data type, same order, same key attributes
- Values are different, at least for the key attributes
- Possible to have several entity sets with the same properties
![[Pasted image 20260908203139.png]]


# ER Model - Attribute
> Attribute describes the property of an entity
- **Key Attribute**: Keys are indicated in ER diagrams by underlining
	- ID
- **Composite** Attribute: A combination of attributes
	- Address
- **Multivalued** Attribute: An attribute that can hold multiple values
	- Phone (Can have multiple phone numbers)
- **Derived** Attribute: Whose value is dynamic and derived from another attribute
	- Age, can be derived from DOB

![[Pasted image 20260908203355.png]]

# ER Model - Relationship
> Association among 2 or more entities
- Uniquely identified by the keys of its entities
	- Lecture **teach** Course
- Relationship may have attributes as well
	- Every tuple of entities connected by the relationship is associated with a value for each attribute
	- Lecture **teach** Course **since** 2022

![[Pasted image 20260908203545.png]]


# Relationship: Participation Constraints
> Specify whether the participation of an entity in a relationship is **compulsory**

Total Participation (Indicated by **BOLD / DOUBLE** lines)
- Each entity in the [[W2 ER Diagram  & SQL#^e62f72|entity set]] is involved in at least 1 relationship
	- Num of relationship in every entity is involved is greater than 0
- Every booking is required to have a customer
	- Participation of **Booking** in this relation is total

Partial Participation (Indicated by **SINGLE** line)
- Each entity in [[W2 ER Diagram  & SQL#^e62f72|entity set]] may or may not occur in at least 1 relationship
- Not every customer needs to have made a booking
	- Participation of **Customer** is partial
![[Pasted image 20260908204212.png]]


## Relationship Cardinality

> Number of associated entities on each side of relationship

- Directed line (->) signifying "One"
- Undirected line (-) signifying "Many"
![[Pasted image 20260908204746.png]]


## Degree of Relationship

> Number of entities involved in relationship

![[Pasted image 20260908204816.png]]

> [!NOTE]
> We usually avoid ternary relationship since, they make up complex logic and business logic that will end up harder to debug and update.

## Weak Entities

> Exist only because of association with strong entities
> - If adult cancels the booking, all dependents booking needs to be canceled.
> - Dependents is an example of a weak **entity** set
> - The attribute name does not identify a dependent uniquely.

![[Pasted image 20260908205024.png]]


## Subclasses and Inheritance

> Represent a more specific type of an existing entity, inheriting its attributes and relationships, while also possessing unique characteristics.

- One entity type might be a subtype of another
- Declare `A ISA B`: Every entity is also considered to be a B entity
- Overlap Constraints
	- Can Joe be both HourlyEmps and a ContractEmps entity?
	- Disallowed. No overlap
- Covering Constraints:
	- Every Employees be an HourlyEmps or a ContractEmps entity ?
	- Yes

![[Pasted image 20260908205318.png]]


![[Pasted image 20260908205406.png]]



![[Pasted image 20260908205418.png]]

> Here you actually have 4 tables: Student, Enrols, Module, Programme
> Grade is under enrols because only when a student enrols to a module do they have a grade


# Integrity Constraints (IC)

> Pre-defined set of rules that are applied on the relations

- ICs come from real-world requirements
	- Specified when schema is defined/created
	- Checked when relations are modified
	- Check database instance to see if certain IC is violated
- Database is legal if all ICs hold for all data
	- DBMS does not allow illegal relations
	- Stored data is more faithful to real-world meaning

## Types of Integrity Constraints

### Domain Constraints

> Restrict the kind of attributes or values a column can hold in the database table

- Every attribute is bound to have a specific range of values
	- Age cannot be less than 0
	- Telephone numbers cannot contain a digit outside 0-9
![[Pasted image 20260908210007.png]]


### Key Constraints

- Only 1 primary key
	- **Unique**: No 2 tuples can have identical values for **Key attributes**
	- **Not NULL**: Key attribute can not have NULL values
![[Pasted image 20260908210111.png]]


### Referential Constraints

The reference from 1 table to another table must be valid
- A foreign key must have a matching primary key
- The reference key element must exist in the table
![[Pasted image 20260908210211.png]]


# Data Types in SQL

- `char(n)`: Fixed length character string
- `varchar(n)`: Variable length character strings, with user-specified maximum length 'n'
- `int`: Integer (Finite subset of integer that is **machine-dependent**)
- `smallint`: Small integer
- `numeric(p, d)`: Fixed point number, with user-specified precision of 'p' digits, with 'd' digits to the right of decimal point (`numeric(3,1)` allows 44.5 to be stored but not 444.5 or 0.32)
- `real, double precision`: Floating point and double-precision floating point
- `float(n)`: Floating point number, with user-specified precision of at least n digits
- `data, time, timestamp`: For values contains date and time
- `blob`: Binary large object, collection of uninterpreted binary data (Interpretation is left to application outside of database system)
- `clob`: Character large object
- `Text`: Very large text, like a full article



## Integrity Constraints in DDL
- primary key ($A_1, ..., A_n$)
- foreign key ($A_m, ..., A_n$) references r
- not null
- default value (Auto-fills a column when no value is given on insert)

### Example
```SQL
create table instructor(
	ID  char(5),
	name  varchar(20) not NULL,
	dept_name  varchar(20),
	salary  numeric(8, 2),
	primary key(ID),
	foreign key (dept_name) references department
);
```




