Relational databases store data in tables, which are organized into rows and columns.
Each row represents a record, and each column represents a field.
The schema of a relational database defines its structure, including tables, columns, [[data types]], and relationships between tables.
uses [[sql]] to create all of it's working parts

# Important keys:
- Primary keys uniquely identify each record in a table.
> [!info]
> Normally you name this as pk_{whatEver}
> They don't have to be a row,  they can be the join of multiple rows
> PRIMARY KEY (name,lastname)

- Foreign keys create a link between two tables, enforcing referential integrity.
	- These are really important for the joins, here is how you (or your [[ORM]]) know where to join the tables

# deep down

To store the data they use B-[[trees]] that are roughly a balanced n-ary tree, they offer efficient data retrieval and insertion.

They are used for indexing, which speeds up data retrieval operations.

The structure of B-trees ensures that data is stored and accessed in a way that minimizes disk reads, enhancing performance.



- The database uses a query optimizer to determine the most efficient way to execute a given query.
- This process involves evaluating different query execution plans and selecting the one with the least estimated cost in terms of resources.