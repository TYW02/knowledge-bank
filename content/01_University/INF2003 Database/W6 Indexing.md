---
title: W6 Indexing
tags:
  - Indexing
---
# Files & File Organization

- A **database** has >= 1 **table**
- A **table** has >= 1 **tuple**, stored in a **data file**
- A **file** has >= 1 data pages (A chunk of **data file**)

> [!information] How DBMS uses Data Pages
> Given a query **requesting** for certain data, DBMS figure out how to **enable efficient access** to the **desired pages** that contain the data.

> [!warning] My Rewrite
> When a query comes in the DBMS will figure out how to efficiently access the data page where the data in contained

## File Organizations

> [!information] What is a File Organization
> Refers to the **logical** and **physical** arrangement of data records in **secondary storage files**.
> - Defines how the DBMS saves, structures, maps and retrieves data blocks to optimize performance for searches, insertions, updates, and deletions

> [!warning] My Rewrite
> Basically means how the data is stored both physically and logically, and the different trade-offs that come with choosing a certain file organization over the other

### Heap File (Random Order)
- Scanning **ALL** records
### Sorted Files
- Good for **order-sensitive** data retrieval and range search.
### Indexes
- Additional data structures to optimize certain retrievals

## Advantages (For good file organization)
- **FAST**
- Speed up search
- Fast updates

# Hash

> [!info] Index is a collection of buckets
> - Bucket: Primary page AND >= 0 **overflow** pages
> - Buckets contain data entries

> [!info] Hashing function h (same for all records)
> - h(r) = bucket in which (data entry for) record r belongs
> - h looks at the search key fields of r

![[Pasted image 20261017183947.png]]


# Tree

## Hash VS Tree
| Hash            | Tree                    |
| --------------- | ----------------------- |
| Equality Search | Equality & Range Search |
| Flat Structure  | Hierarchy               |

- Both **direct** a search to a suitable **page**

## B+ Tree

> [!info] Basic Elements
> - Root
> - Internal Nodes (Non-leaf)
> - Leaves

- High fanout (Typically on order of 100 or more)

> [!info] What is Fanout ?
> Number of **pointers to child nodes** in a node


> [!failure] Important Rules
> - **ALL data** is in the leaf node
> - **Leaves** all in the **same level**
> 	- Tree **balance** is important
> - Leaves are **linked** together
> - Each leaf node, `k` keys, and `k+1` pointers
> - **Minimum** 50% occupancy, Root is an exception

## B+ Tree: Search
![[Pasted image 20261017184610.png]]


## B+ Tree: Insert

> [!important] Order of insert
> Locate -> Insert -> Update
> - Insert value into leaf. **Is there enough space** ?
> 	- True: Done
> 	- False: **Split** the leaf into 2 new nodes
> 		- Redistribute **evenly**
> 		- Add **parent node** new key (Duplicate min value of the 2nd new node)
> - Recursive execution. Level by level until no split is needed
> - Tree can grow, wider, deeper. (**DO NOT** violate the **min occupancy**)
> 

![[Pasted image 20261017184915.png]]

![[Pasted image 20261017185001.png]]


## B+ Tree: Delete

> [!important] Order of delete
> Locate -> Remove -> Low Occupancy ?
> 	- True: Done
> 	- False: Try **borrowing** one from **nearest siblings**, if cannot, **merge**
> - Recursive. Level by level (upwards) until no changes needed.
> - Tree can be smaller


![[Pasted image 20261017185219.png]]
> No Changes here since the leaf node with 8 still has enough occupancy

![[Pasted image 20261017185314.png]]


![[Pasted image 20261017185356.png]]





































