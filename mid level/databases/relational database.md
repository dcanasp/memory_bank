Relational databases store data in **tables**, consisting of **rows** (records) and **columns** (fields). The **schema** of a relational database defines its structure, including tables, columns, [[data types]], and the relationships between tables (and functions or triggers). [[SQL]] is used to manage and query the data.


These databases are ideal for complex tasks requiring certainty and intricate relationships, such as a social network where users, followers, comments, etc., are interconnected.
# theory
## ACID

Another great thing is that relational databases are ACID compliant, this means they follow this rules:
1. **Atomicity:**
	- the **transaction** (changes) completes in its entirety without failures or the transaction is reverted. There is no case where only half the writes are changed leading to inconsistency.
2. **Consistency:**
	- Consistency ensures that a transaction brings the database from one valid state to another. The database must satisfy a set of integrity constraints before and after the transaction. If a transaction violates any integrity constraints, it is rolled back, preserving the consistency of the database.
3. **Isolation:**
    - All read and write requests within a transaction are not impacted by other transactions. This ensures that the changes being made in one transaction are not available in other transactions.
4. **Durability:**
    - Durability ensures that once a transaction is committed, its changes are **permanent** and will survive subsequent failures. The committed changes are stored in a durable medium, such as disk storage, and are not lost even if the system crashes. This property guarantees that the database can recover to a consistent state after a failure.
### Read Phenomena
defined at the The ANSI/ISO standard SQL 92. Are common isolation problem that can occur on relational database transactions
1. **Dirty Reads** When concurrent transactions can read changes not committed yet. 
2. **Non-repeatable Reads** When a single transaction gets different read values on the same data, something changed
3. **Phantom Reads** Similar to the previous, when a single transaction asks for a set of data (all users with the name `david`) multiple times get a different set of data.
4. **Lost Updates or Serialization Anomaly** When two transactions that modify the same data start at a similar time, one will commit it's changes, the other will also commit it's changes rewriting over the previous transaction. a problem with parallelism
### Isolation levels
To solve these problems relational databases have implemented 3/4 transaction levels. These will prevent/allow the read Phenomena in the same order.
1. **Read Uncommitted**: allows all read phenomena
2. **Read Committed**: prevents up to 1. (dirty reads)
3. **Repeatable Read**: prevents up to 3. (Non-repeatable Reads and Phantom Reads)
4. **Serializable**: prevents up to 4. (Serialization Anomaly)
These are in increasing order, so a level 4 serializable will solve all of the read phenomena, and a level 3 will solve the first three only

>[!important]
>Those levels i've written are exclusive for *MariaDb*/*MySql*. *Postgres* only has 3 levels, as it will never allow Dirty Reads on the image are the actual *Postgres* isolation levels
>![[postgres_IsolationLevels.png]]

Now it's important to understand that this is a standard. Each database will implement it in a different way. *MariaDb*/*Mysql* will set the isolation level on each session, meanwhile *postgres* will set the **isolation** level for each **transaction**.

some other important facts are that *MariaDb*/*Mysql* will use a lock mechanism meanwhile *Postgres* will use dependencies detection. Also a higher isolation level will generate more errors (as it will prevent modification on more cases than a lower isolation level), therefore if you want to implement a higher isolation you should also implement retry mechanisms. Finally a higher isolation level will be slower, as it will have to do more work for a single transaction


## deep down

To store the data they use B-[[trees]] that are roughly a balanced n-ary tree, they offer efficient data retrieval and insertion.

They are used for **indexing**, which speeds up data retrieval operations.

The structure of B-trees ensures that data is stored and accessed in a way that minimizes disk reads, enhancing performance.

- The database uses a query optimizer to determine the most efficient way to execute a given query.
- This process involves evaluating different query execution plans and selecting the one with the least estimated cost in terms of resources.


They also have another distinction, **denormalized** vs **normalized** databases. Normalized databases are designed to minimize redundancy, while denormalized databases are designed to optimize read time.

in normalized databases, you save the references as foreign keys, so there are no repeated data, but on denormalized databased, you would store the references as data, so it is faster
# practice
to understand this you need to know [[SQL]]
## Important keys:
- **Primary keys** uniquely identify each record in a table.
> [!info]
> Normally you name this as pk_{whatEver}
> They don't have to be a row,  they can be the join of multiple rows
> PRIMARY KEY (name,lastname)

- **Foreign keys** create a link between two tables, enforcing referential integrity.
	- These are really important for the joins, here is how you (or your [[ORM]]) know where to join the tables

## indexes
Indexes are used to **speed up** data retrieval operations in a database. They work much like an index in a book, allowing the database to **find** data **without scanning** every row of a table.

Commonly implemented using B-[[trees]], which balance efficient data retrieval and insertion while minimizing disk reads. An index can be created on **one** or **more** **columns** of a table.

## relationships
in between tables you can have relationships with **foreign keys**, this relationships can be of types:  
### one to one
when one value has a relation to only one other value. This mostly are saved on the same table in a different collumm, For example one user only has one unique ID
### one to many
When one value relates to multiple ones on the second table. For example in a news DB. a user can have multiples articles written, so in the articles table, there is a foreign key to that unique user 
### many to many
Many-to-many relationships occur when multiple records in a table relate to multiple records in another table. To solve this you have to Implement a **associative table** (junction table) that holds foreign keys referencing the primary keys of the related tables.

- Example: In a book-author relationship, a book can have multiple authors, and an author can write multiple books.

## Triggers

Triggers are automated **procedures** initiated in **response** to specific events on a particular table or view in the database.

- **Functionality**:
    - **Execute** automatically before or **after** data **modification** (INSERT, UPDATE, DELETE).
    - Useful for maintaining data integrity, **enforcing business rules**, and auditing changes.
- **Types**:
    - **Before Triggers**: Execute before the triggering statement, allowing the opportunity to validate or change data before it's committed.
    - **After Triggers**: Execute after the triggering statement, suitable for logging, auditing, or other post-operation analysis.
- **Considerations**:
    - Triggers can greatly affect database performance and should be used judiciously.
    - Debugging can be more complex due to their implicit nature.

## Functions

Functions are modules of [[SQL]] code that encapsulate a particular operation or a set of operations.

They can **return** a single **value** or a **table**. Functions that **return** a **table** are often called **stored procedures**. These are used to encapsulate repetitive or complex logic, making the database more modular and efficient.

- **Uses**:
    - Data **validation**, data **transformation**, and complex business logic implementation.
    - Can be invoked in SQL queries to operate on data and return results.
- **Types**:
    - **Scalar Functions**: Return a single value, based on input parameters.
    - **Table-Valued Functions**: Return a table and can be used in a SELECT statement like any other table.
- **Advantages**:
    - Promotes code reuse and simplifies maintenance.
    - Enhances security by encapsulating the business logic and allowing controlled data access.
