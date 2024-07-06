### SQL Commands and Their Types (with MySQL Examples)

**SQL Commands:**
SQL commands are instructions used to communicate with a database to perform specific tasks, work with data, and manage database structures.

**Types of SQL Commands:**

1. **Data Manipulation Language (DML):**
   - **INSERT:** Adds new records to a table.
   - **UPDATE:** Modifies existing records in a table.
   - **DELETE:** Removes records from a table.
   - **SELECT:** Retrieves data from one or more tables.

2. **Data Definition Language (DDL):**
   - **CREATE:** Creates new tables, databases, or other database objects.
   - **ALTER:** Modifies the structure of an existing table.
   - **DROP:** Deletes tables, databases, or other database objects.

3. **Data Control Language (DCL):**
   - **GRANT:** Gives user access privileges to the database.
   - **REVOKE:** Removes user access privileges to the database.

4. **Transaction Control Language (TCL):**
   - **COMMIT:** Saves the changes made by the current transaction.
   - **ROLLBACK:** Reverts the changes made by the current transaction.
   - **SAVEPOINT:** Sets a point within a transaction to which you can later roll back.

### DML Commands (with MySQL Examples)

**INSERT:**
- **Definition:** Adds new records to a table.
- **Example:**
  ```sql
  INSERT INTO Employees (EmployeeID, Name, DepartmentID)
  VALUES (1, 'John Doe', 101);
  ```

**UPDATE:**
- **Definition:** Modifies existing records in a table.
- **Example:**
  ```sql
  UPDATE Employees
  SET DepartmentID = 102
  WHERE EmployeeID = 1;
  ```

**DELETE:**
- **Definition:** Removes records from a table.
- **Example:**
  ```sql
  DELETE FROM Employees
  WHERE EmployeeID = 1;
  ```

**SELECT:**
- **Definition:** Retrieves data from one or more tables.
- **Example:**
  ```sql
  SELECT * FROM Employees;
  ```

### DDL Commands (with MySQL Examples)

**CREATE:**
- **Definition:** Creates new tables, databases, or other database objects.
- **Example:**
  ```sql
  CREATE TABLE Employees (
      EmployeeID INT PRIMARY KEY,
      Name VARCHAR(100),
      DepartmentID INT
  );
  ```

**ALTER:**
- **Definition:** Modifies the structure of an existing table.
- **Example:**
  ```sql
  ALTER TABLE Employees
  ADD COLUMN Email VARCHAR(100);
  ```

### Operators and Aggregation in SQL

**Operators:**
- **Arithmetic Operators:** +, -, *, /
  ```sql
  SELECT 10 + 5;
  ```

- **Comparison Operators:** =, <>, >, <, >=, <=
  ```sql
  SELECT * FROM Employees WHERE DepartmentID = 101;
  ```

- **Logical Operators:** AND, OR, NOT
  ```sql
  SELECT * FROM Employees WHERE DepartmentID = 101 AND Name = 'John Doe';
  ```

**Aggregation:**
- **Definition:** Functions that perform calculations on a set of values and return a single value.
- **Example:**
  ```sql
  SELECT COUNT(*) AS EmployeeCount FROM Employees;
  SELECT AVG(Salary) AS AverageSalary FROM Employees;
  SELECT SUM(Salary) AS TotalSalary FROM Employees;
  ```

### SQL Clauses (with MySQL Examples)

**WHERE:**
- **Definition:** Filters records based on specified conditions.
- **Example:**
  ```sql
  SELECT * FROM Employees WHERE DepartmentID = 101;
  ```

**GROUP BY:**
- **Definition:** Groups rows that have the same values in specified columns.
- **Example:**
  ```sql
  SELECT DepartmentID, COUNT(*) AS EmployeeCount
  FROM Employees
  GROUP BY DepartmentID;
  ```

**HAVING:**
- **Definition:** Filters groups based on specified conditions.
- **Example:**
  ```sql
  SELECT DepartmentID, COUNT(*) AS EmployeeCount
  FROM Employees
  GROUP BY DepartmentID
  HAVING COUNT(*) > 10;
  ```

**ORDER BY:**
- **Definition:** Sorts the result set by one or more columns.
- **Example:**
  ```sql
  SELECT * FROM Employees
  ORDER BY Name ASC;
  ```

**LIMIT:**
- **Definition:** Specifies the number of records to return.
- **Example:**
  ```sql
  SELECT * FROM Employees
  LIMIT 5;
  ```

### Joins in SQL (with MySQL Examples)

**INNER JOIN:**
- **Definition:** Returns records that have matching values in both tables.
- **Example:**
  ```sql
  SELECT Employees.Name, Departments.DepartmentName
  FROM Employees
  INNER JOIN Departments ON Employees.DepartmentID = Departments.DepartmentID;
  ```

**LEFT JOIN:**
- **Definition:** Returns all records from the left table and matched records from the right table.
- **Example:**
  ```sql
  SELECT Employees.Name, Departments.DepartmentName
  FROM Employees
  LEFT JOIN Departments ON Employees.DepartmentID = Departments.DepartmentID;
  ```

**RIGHT JOIN:**
- **Definition:** Returns all records from the right table and matched records from the left table.
- **Example:**
  ```sql
  SELECT Employees.Name, Departments.DepartmentName
  FROM Employees
  RIGHT JOIN Departments ON Employees.DepartmentID = Departments.DepartmentID;
  ```

**FULL OUTER JOIN:**
- **Definition:** Returns all records when there is a match in either left or right table.
- **Example:** Note: MySQL does not directly support FULL OUTER JOIN.
  ```sql
  SELECT Employees.Name, Departments.DepartmentName
  FROM Employees
  LEFT JOIN Departments ON Employees.DepartmentID = Departments.DepartmentID
  UNION
  SELECT Employees.Name, Departments.DepartmentName
  FROM Employees
  RIGHT JOIN Departments ON Employees.DepartmentID = Departments.DepartmentID;
  ```

### Unions in SQL

**Definition:**
- Combines the result sets of two or more SELECT statements.

**Example:**
```sql
SELECT Name FROM Employees
UNION
SELECT Name FROM Contractors;
```

### Views in SQL

**Definition:**
- A virtual table based on the result set of an SQL query.

**Example:**
```sql
CREATE VIEW EmployeeView AS
SELECT Employees.Name, Departments.DepartmentName
FROM Employees
INNER JOIN Departments ON Employees.DepartmentID = Departments.DepartmentID;
```

### SQL Sub Queries

**Definition:**
- A query nested inside another query.

**Example:**
```sql
SELECT Name
FROM Employees
WHERE DepartmentID = (SELECT DepartmentID FROM Departments WHERE DepartmentName = 'HR');
```

### Example Interview Questions

1. **What is the difference between `INNER JOIN` and `LEFT JOIN`?**
   - **Answer:** `INNER JOIN` returns only the rows with matching values in both tables, while `LEFT JOIN` returns all rows from the left table and the matched rows from the right table.

2. **How would you retrieve the top 5 highest-paid employees from a table?**
   - **Answer:** Use the `SELECT` statement with `ORDER BY` and `LIMIT`.
     ```sql
     SELECT * FROM Employees
     ORDER BY Salary DESC
     LIMIT 5;
     ```

3. **Explain the use of the `GROUP BY` clause.**
   - **Answer:** `GROUP BY` is used to group rows that have the same values in specified columns and often used with aggregation functions.
     ```sql
     SELECT DepartmentID, COUNT(*) AS EmployeeCount
     FROM Employees
     GROUP BY DepartmentID;
     ```

4. **What is a subquery, and when would you use one?**
   - **Answer:** A subquery is a query nested inside another query, used to perform operations that require data from multiple queries.
     ```sql
     SELECT Name
     FROM Employees
     WHERE DepartmentID = (SELECT DepartmentID FROM Departments WHERE DepartmentName = 'HR');
     ```

5. **What is the difference between `UNION` and `UNION ALL`?**
   - **Answer:** `UNION` removes duplicate records, while `UNION ALL` includes duplicates.
     ```sql
     SELECT Name FROM Employees
     UNION
     SELECT Name FROM Contractors;

     SELECT Name FROM Employees
     UNION ALL
     SELECT Name FROM Contractors;
     ```

6. **How do you create a view, and why would you use one?**
   - **Answer:** A view is created using the `CREATE VIEW` statement and is used to simplify complex queries or to provide a specific view of the data for security purposes.
     ```sql
     CREATE VIEW EmployeeView AS
     SELECT Employees.Name, Departments.DepartmentName
     FROM Employees
     INNER JOIN Departments ON Employees.DepartmentID = Departments.DepartmentID;
     ```
