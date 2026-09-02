---
title: W1 DB & Relational Model
tags:
  - ACID
---
# Database
An organized collection of information

- Database Management System (DBMS)
	- Software package designed to store and manage database
	- Provides data processing environment that is both convenient and efficient to use
	- Address all complications in data management
	- Basic Operations: Create, Read, Update, Delete (CRUD)


## Why DBMS
![[Pasted image 20260902081000.png]]


## DBMS Data Abstraction

**View** Level (External) For users, developers
- User performs queries and operations, often in a software

**Logical** Level (Conceptual) For Developers, DB admin
- Communication protocol, define the abstracted structure (How data pieces relate to one another)

**Physical** Level (Internal) For DB Admin
- How data stored in disk, memory, cache, etc..

> Data is relatively isolated in different levels -> Data independence


## DBMS Data Independence

### Physical Independence
Change the physical characteristics without affecting the conceptual level
- Modify the physical schema
- Data is stored on disk or magnetic tapes
- Changes to compression techniques or hashing algorithms

### Logical Independence
Change the logic structure of the data without affecting the other layers of the database
- Add/Modify/Delete a new attribute, entity or relationship is possible without a rewrite of existing application programs
- Merging 2 records into 1
- Breaking an existing record into 2 or more records


# DBMS Architecture
![[Pasted image 20260902081559.png]]



# Relational DB standard in transaction: ACID
#ACID

## Atomicity
- The entire transaction takes place at once or not at all
## Consistency
- Database must be consistent before and after transaction
## Isolation 
- Multiple transactions occur independently without interference
## Durability
- Once a transaction is committed, considered permanent, even when there is a system failure



# Relational Data Model
- A collection of relations, each has a unique name
- Relation (A table with rows and columns)
	- Each row in the table specifies a relationship between the values in that row 
	- Simple data representation
	- Easy query, expressing what you want
- Relations are unordered
	- Allows optimized storage


## Relational Schema
- Every relation has a schema
	- Specifies the type of information for relations (Attribute name, domain)
	- Different relations can share the same schema
- Relation schema includes
	- Set of attributes
	- Domain of each attribute
- Notation: r(R) the schema of r is R
	- STUDENT(sid, sname, saddress)
		- r: STUDENT
		- R: (sid, sname, saddress)
	- Domains are not stated explicitly in this notation


## Domain: NULL
- What NULL is
	- A member of every domain: the value is unknown or not applicable
	- Comparing **ANYTHING** with NULL yields UNKNOWN, not true or false
- Common traps
	- WHERE age = NULL never matches a row (use IS NULL / IS NOT NULL)
	- A WHERE clause keeps a row only if it is TRUE, so UNKNOWN rows are dropped
	- COUNT(age) skips NULLs, COUNT(\*) does not 
	- Arithmetic with NULL is NULL (Salary + bonus is NULL if bonus is unknown)


## Avoid Duplication (Keys)
- Keys are used to distinguish individual tuples
- A certain minimal subset of relation attributes uniquely identifies a tuple
	- Keys define the meaning of the relation
	- All relations have a key, some may have multiple keys
	- Unique: 2 distinct tuples **CANNOT** have same values in all key attributes

- **Superkey**: Set of attribute within a table that **CAN** uniquely identify each record
	- Not all superkeys are equally useful
- **Candidate Key**: Minimal set of fields which can uniquely identify each record
	- There can be more than 1 candidate key
- **Primary Key**: Candidate key that is most appropriate to become the main key
	- How to indicate Primary Key? (Underline it)
STUDENT(<u>sid</u>, sname, saddress, sphone)
![[Pasted image 20260902082833.png]]


## Foreign Key
- To link data among relations/tables
	- Foreign key is the primary key of the other relations
	- Referencing relation and referenced relation, Like a pointer
### Example
sid is a foreign key referring to STUDENT:
![[Pasted image 20260902082945.png]]


# Stages of Database Design

## Requirement Analysis
> [!Interviews reveal]
> A student enrolls in many modules, each module caps at 40 seats, and 8000 students hit the system in 1 enrolment week.

## Conceptual Database Design
> [!ER Diagram]
> STUDENT -> Enrolls -> MODULE
> as an M:N relationship, with Grade as an attribute of the relationship itself.
![[Pasted image 20260902083202.png]]

## Logical Database Design
> [!Map ER to relations]
> Student(matricid, name, programme),
> Module(code, title, lecturer, lecturerOffice),
> Enrolls(matricid, code, grade)

## Refine the Schemas
> [!Analyze -> identify potential problem -> refine]
> Module(code, title, lecturer, lectuererOffice)
> It has a transitive dependency
> Decompose:
> Module(code, titile, lecturerId) -> lectuererId is now a foriegn key
> Lecturer(lecturerId, name, office)

## Physical Database Design
> [!Make the common queries fast]
> Enrolls(matricid, code, grade)
> Students tap "Show my Modules" all day. Without help, the database reads every row in Enrolls to find 1 student's
> An index on the 'matricid' jumps straight to them, like a book index instead of reading every page.

## Application and Security Design
> [!Security First]
> A student SELECTs only their own row via a view;
> Only the registrar is GRANTED update on grade;
> Enrolment runs in a serialisable transaction.














