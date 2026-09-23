> Guarantee database transactions are processed reliably.
# Atomicity
The entire transaction takes place at **once or not at all**
# Consistency
Database must be consistent **before** and **after** transactions
# Isolation
**Multiple** transactions occur **independently** without interference
# Durability
Once a transaction is **committed**, considered **permanent**, even when there is **system failure**.


## DBMS Rollback
- Atomicity

> Atomicity enforces an '**all-or-nothing**' execution rule, ensuring that if **any part** of a transaction **fails**, all previous steps are **completely aborted and undone**.



