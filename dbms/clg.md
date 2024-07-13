
### Constraints in MySQL

**Types of Constraints:**
1. **NOT NULL**: Ensures that a column cannot have a NULL value.
   ```sql
   CREATE TABLE example (
       id INT NOT NULL,
       name VARCHAR(100) NOT NULL
   );
   ```

2. **UNIQUE**: Ensures all values in a column are different.
   ```sql
   CREATE TABLE example (
       id INT NOT NULL UNIQUE,
       name VARCHAR(100) NOT NULL
   );
   ```

3. **PRIMARY KEY**: A combination of `NOT NULL` and `UNIQUE`. Uniquely identifies each row in a table.
   ```sql
   CREATE TABLE example (
       id INT PRIMARY KEY,
       name VARCHAR(100)
   );
   ```

4. **FOREIGN KEY**: Ensures the referential integrity of the data in one table to match values in another table.
   ```sql
   CREATE TABLE example (
       id INT PRIMARY KEY,
       dept_id INT,
       FOREIGN KEY (dept_id) REFERENCES department(dept_id)
   );
   ```

5. **CHECK**: Ensures that the values in a column meet a specific condition (Note: CHECK is not enforced in MySQL).
   ```sql
   CREATE TABLE example (
       id INT,
       age INT CHECK (age >= 18)
   );
   ```

6. **DEFAULT**: Sets a default value for a column when none is specified.
   ```sql
   CREATE TABLE example (
       id INT,
       created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
   );
   ```

### Types to Define Primary Key

1. **Single Column Primary Key:**
   ```sql
   CREATE TABLE example (
       id INT PRIMARY KEY,
       name VARCHAR(100)
   );
   ```

2. **Composite Primary Key:**
   ```sql
   CREATE TABLE example (
       id INT,
       name VARCHAR(100),
       PRIMARY KEY (id, name)
   );
   ```

### References Options

When defining a `FOREIGN KEY`, you can specify options like `ON DELETE` and `ON UPDATE` to determine what happens when the referenced data is deleted or updated:

1. **CASCADE**: Deletes or updates the row in the child table when the row in the parent table is deleted or updated.
   ```sql
   FOREIGN KEY (dept_id) REFERENCES department(dept_id) ON DELETE CASCADE ON UPDATE CASCADE
   ```

2. **SET NULL**: Sets the foreign key column to NULL when the referenced row is deleted or updated.
   ```sql
   FOREIGN KEY (dept_id) REFERENCES department(dept_id) ON DELETE SET NULL ON UPDATE SET NULL
   ```

3. **RESTRICT**: Prevents the delete or update operation on the referenced table.
   ```sql
   FOREIGN KEY (dept_id) REFERENCES department(dept_id) ON DELETE RESTRICT ON UPDATE RESTRICT
   ```

4. **NO ACTION**: Similar to `RESTRICT` but differs in the timing of the check.
   ```sql
   FOREIGN KEY (dept_id) REFERENCES department(dept_id) ON DELETE NO ACTION ON UPDATE NO ACTION
   ```


### Difference Between TRUNCATE and DELETE

- **TRUNCATE**:
  - Removes all rows from a table.
  - Cannot be rolled back.
  - Resets auto-increment counter.
  - Faster than DELETE as it does not generate individual row delete actions.
  - Does not fire triggers.
  
  ```sql
  TRUNCATE TABLE example;
  ```

- **DELETE**:
  - Removes rows from a table based on a condition.
  - Can be rolled back.
  - Does not reset auto-increment counter.
  - Slower than TRUNCATE.
  - Fires triggers.

  ```sql
  DELETE FROM example WHERE id = 1;
  ```

### Clauses Types with Examples

1. **WHERE**: Filters records.
   ```sql
   SELECT * FROM employee WHERE dept_id = 1;
   ```

2. **ORDER BY**: Sorts records.
   ```sql
   SELECT * FROM employee ORDER BY emp_name ASC;
   ```

3. **GROUP BY**: Groups records with the same values.
   ```sql
   SELECT dept_id, COUNT(*) FROM employee GROUP BY dept_id;
   ```

4. **HAVING**: Filters records after grouping.
   ```sql
   SELECT dept_id, COUNT(*) FROM employee GROUP BY dept_id HAVING COUNT(*) > 5;
   ```

5. **LIMIT**: Specifies the number of records to return.
   ```sql
   SELECT * FROM employee LIMIT 10;
   ```

### Pattern Matching Types with Example

1. **LIKE**: Finds values that match a specified pattern.
   - `%` matches any number of characters.
   - `_` matches a single character.
   
   ```sql
   SELECT * FROM employee WHERE emp_name LIKE 'A%';
   ```

2. **REGEXP**: Finds values that match a regular expression.
   
   ```sql
   SELECT * FROM employee WHERE emp_name REGEXP '^A';
   ```

### BETWEEN()

The `BETWEEN` operator selects values within a given range. The values can be numbers, text, or dates.

```sql
SELECT * FROM employee WHERE emp_id BETWEEN 1 AND 10;
```
### Views

A view is a virtual table based on the result-set of an SQL statement. It contains rows and columns just like a real table.

```sql
CREATE VIEW employee_dept AS
SELECT employee.emp_name, department.dept_name
FROM employee
INNER JOIN department ON employee.dept_id = department.dept_id;
```

You can query a view just like a table:
```sql
SELECT * FROM employee_dept;
```
