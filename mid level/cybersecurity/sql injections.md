
**SQL Injection** is a type of security vulnerability that occurs in the database layer of an application. It allows attackers to interfere with the queries an application makes to its database. It usually involves inserting or "injecting" malicious SQL code into a query.

### How It Happens

- **User Input Manipulation**: The vulnerability typically occurs when user input is not properly sanitized and is directly used in SQL queries. This can lead to malicious SQL being executed.
- **Examples**: Entering a string like `'; DROP TABLE users;--` in a form field that directly influences a database query.

### Consequences

- **Data Breach**: Unauthorized viewing, extraction, or deletion of data.
- **Database Manipulation**: Altering or dropping tables.
- **System Compromise**: In severe cases, attackers can gain administrative access to the database [[server]].

### Prevention

**Input Validation**: Ensure all user input is validated for type and format.
**Prepared Statements**: Use prepared statements with parameterized queries.
**Stored Procedures**: Encapsulate SQL in stored procedures, which also helps in managing permissions.
**[[ORM]]**: Most of them already keep you save from this attack

### Examples

- **Safe Query (using Prepared Statement)**:
    

```sql
    SELECT * FROM users WHERE username = ?
 ```   
    
Here, the `?` is a placeholder for a parameter whose value is safely added by the database system.
    
- **Unsafe Query**:
    
    
```sql
	SELECT * FROM users WHERE username = '" + userInput + "';
```
    
In this case, `userInput` is directly concatenated, making the query vulnerable.
    
