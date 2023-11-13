SQL is a domain-specific language used in programming and designed for managing data held in a relational database management system (RDBMS), or for stream processing in a relational data stream management system (RDSMS).

### Key Components of SQL

1. **Data Definition Language (DDL)**: This includes commands such as `CREATE`, `DROP`, `ALTER`, etc., used to define or modify data structures and database schemas.
    
2. **Data Manipulation Language (DML)**: This encompasses commands like `INSERT`, `UPDATE`, `DELETE`, etc., which are used to manipulate data within the database tables.
    
3. **Data Query Language (DQL)**: Central to SQL, it involves the `SELECT` query, which is used to fetch data from a database. This can be highly sophisticated with joins, subqueries, and complex conditions.
    
4. **Data Control Language (DCL)**: This includes commands like `GRANT` and `REVOKE`, which are used to control access to data in the database.
    
5. **Transaction Control Language (TCL)**: Commands like `COMMIT` and `ROLLBACK` fall under this category, dealing with transaction management in a database.
    

### Advanced Concepts

1. **Joins and Relationships**: Understanding different types of joins (INNER, LEFT, RIGHT, FULL) is crucial for querying data from multiple tables.
    
2. **Indexes and Performance Tuning**: Creating and managing indexes is essential for optimizing query performance.
    
3. **Stored Procedures and Functions**: These are sets of SQL statements that can be stored in the server. Stored procedures are invoked and executed as a unit, while functions can return values.
    
4. **Triggers**: Triggers are SQL commands that are automatically executed in response to certain events on a particular table or view.
    
5. **Normalization**: It's the process of organizing data to minimize redundancy. Normalization typically involves dividing large tables into smaller, and less redundant tables and defining relationships between them.
    
6. **ACID Properties**: Ensuring Atomicity, Consistency, Isolation, and Durability in transactions is vital for the integrity of databases.
    
7. **SQL in Distributed Databases**: Understanding how SQL is implemented in distributed databases, like sharding, replication, and CAP theorem considerations.
    

it's important to note that each [[database manager]] have their SQL dialects and specific features/extensions. This is specially notable with oracle (and what ever they are doing over there)
