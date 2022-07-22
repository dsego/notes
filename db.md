# Interview Questions
- https://www.toptal.com/sql/interview-questions
- http://www.indiabix.com/technical/sql-server-common-questions/


## HEAP
- Tables with no indexes, not ordered, searched by scanning.
- IAM - index allocation map that points to all pages
- Data pages - as many rows as can fit
- No linking between pages, reads and writes consult IAM

## IAM
- Each IAM page contains one huge bitmap, tracking 511,232 pages, or about 4 GB of data.
- IAM page doesn’t track the individual pages, but rather groups of eight, known as extents
- If > 4GB = creates new IAM page


## CLUSTERED INDEX

- Stored as a B-tree (binary tree), physically orders pages
- Root node -> index nodes -> leaf nodes
- Leaf nodes store rows of data
- Only one per table (can be on multiple columns)
- Pages reference each other via linked list pointers


- PRIMARY KEY creates a clustered index by default
    - **DOWNSIDE - Page Split** when inserting, page split is a costly operation
    - avoid by never inserting new rows between existing ones (auto-increment identity key)


## NONCLUSTERED INDEX

- B-tree with the index key values and pointers to the data rows
- The index is pointing to the actual data (RID - row identifier)
- UNIQUE KEY creates a nonclustered index by default


## CONSTRAINTS

- NOT NULL
- UNIQUE       - multiple per table,
- PRIMARY KEY  - only one per table, does not allow NULL or duplicate values
- FOREIGN KEY -  enforces referential integrity
    - ON UPDATE or ON DELETE
        * RESTRICT / NO ACTION   - operation in the parent table will fail with an error
        * CASCADE                - operation reflected to the related values in the child table
        * SET NULL               - all related values in the child table are set to NULL value
        * SET DEFAULT

- CHECK constraint is used to limit the values that can be placed in a column


## NORMALIZATION

Database schema design approach for relational databases.

Normalizing principles to:

- reduce the duplication of data
- avoid data anomalies
- ensure referential integrity
- simplify data management

## Referential integrity

Foreign key reference a primary key or null.

### Unnormalized:
- Lacks atomic data -> not relational
  ( more than one value is stored in a single attribute within a row/tuple )
- Repeated data - insert/update/delete anomalies

### 1NF
- Each record is unique (no duplicate rows, primary key)
- Each column (cell) contains one value

### 2NF
- All non-key attributes are fully functional dependent on the primary key
  (single primary key)

### 3NF
- Has no transitive functional dependencies

-------------------------------------
    the Key - 1NF
    the whole key - 2NF
    nothing but the key - 3NF
-------------------------------------


## BCNF (3.5 NF) - Boyce-Codd
## 4NF
## 5NF
## 6NF


## PARTITIONING

* Vertical   = large table -> multiple smaller tables with different columns
* Horizontal = same columns, but different rows
               usually based on column (eg datetime, range partitioning)


## ACID

* Atomicity - transaction succeeds completely, or fails completely
* Consistency - keeps valid state (constraints, cascades, triggers)
* Isolation - concurrency control (same state as sequential)
* Durability - persistent storage

## TRANSACTION

- reliable units of work that allow correct recovery from failures and keep a database consistent
- isolation between programs accessing a database concurrently
- must be ACID (atomic, consistent, isolated, durable)


## DEADLOCK

- Two or more transactions are waiting indefinitely for one another to give up locks
- Prevention (compare time stamps):
    * Wait-die scheme: Wait if older or die if younger.
    * Wound-wait scheme: wound younger one = force to be rolled back, or wait


