# Theory
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

# Practice

here are some of the most common commands 
## main commands
### `CREATE` - Creating Database Objects
- **Table Creation:**
```sql
CREATE TABLE employees (
    emp_id INT PRIMARY KEY,
    emp_name VARCHAR(255),
    emp_salary DECIMAL(10, 2)
);
```

### `DROP` - Deleting Database Objects
- **Table Deletion:**
```sql
DROP TABLE employees;
```
### `ALTER` - Modifying Database Objects
- **Adding a Column:**
    `ALTER TABLE employees ADD COLUMN emp_department VARCHAR(50);`
```sql
ALTER TABLE employees
ADD COLUMN emp_department VARCHAR(50);
```
  
### `INSERT` - Adding Data to a Table
- **Inserting a Record:**
```sql
INSERT INTO employees (emp_id, emp_name, emp_salary)
VALUES (1, 'John Doe', 50000.00);
```
  
### `UPDATE` - Modifying Existing Data
- **Updating Records:**
    ```sql
UPDATE employees
SET emp_salary = 55000.00
WHERE emp_id = 1;
```

### `DELETE` - Removing Data from a Table
- **Deleting Records:**
```sql
DELETE FROM employees
WHERE emp_id = 1;
```
  
### `SELECT` - Retrieving Data
- **Basic Query:**
```sql
SELECT emp_id, emp_name
FROM employees;
```

### `GRANT` - Assigning Privileges
- **Granting SELECT Privilege:**
```sql
GRANT SELECT ON employees TO user1;
```

### `REVOKE` - Revoking Privileges
- **Revoking SELECT Privilege:**
```sql
REVOKE SELECT ON employees FROM user1;
```
  
### `COMMIT` - Committing Transactions
- **Committing Changes:**
    `COMMIT;`

### `ROLLBACK` - Rolling Back Transactions
- **Rolling Back Changes:**
    `ROLLBACK;`

## Join Operations

### INNER JOIN
- Combines rows from two or more tables based on a related column.

```sql
SELECT employees.emp_id, employees.emp_name, departments.department_name
FROM employees
INNER JOIN departments ON employees.department_id = departments.department_id;
```
## Triggers

- Triggers are database objects that automatically perform actions in response to certain events on a particular table or view.

```sql
CREATE TRIGGER before_employee_insert
BEFORE INSERT ON employees
FOR EACH ROW
BEGIN
  -- Trigger logic here
  IF NEW.emp_salary < 50000.00 THEN
    SET NEW.emp_salary = 50000.00;
  END IF;
END;
```

## Indexes
- Indexes improve the speed of data retrieval operations on a database table.
```sql
CREATE INDEX idx_emp_name ON employees (emp_name);
```