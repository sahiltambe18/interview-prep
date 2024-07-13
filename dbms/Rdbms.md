### Relational Database Management System (RDBMS)

**What is RDBMS?**
- **Definition:** RDBMS stands for Relational Database Management System. It is a type of database management system (DBMS) that stores data in a structured format, using rows and columns. This approach makes it easy to retrieve and manipulate data.
- **Example:** MySQL is a popular RDBMS used in many web applications.

**Key Features of RDBMS:**
- **Tables:** Data is organized into tables.
- **SQL:** Uses Structured Query Language (SQL) for querying and maintaining the database.
- **ACID Properties:** Ensures transactions are processed reliably.

**Example Question:** What is an RDBMS, and how is it different from a DBMS?
- **Answer:** An RDBMS is a type of DBMS that organizes data into tables (relations) and uses SQL for database access. It supports ACID properties to ensure data integrity and reliability, which may not be fully supported by all DBMS types.

### Essential Components of a Table

1. **Columns (Attributes):**
   - **Definition:** Define the type of data stored in each part of the table.
   - **Example:** In a "Students" table, columns might include StudentID, Name, and DateOfBirth.
   - **SQL Example:**
     ```sql
     CREATE TABLE Students (
         StudentID INT,
         Name VARCHAR(100),
         DateOfBirth DATE
     );
     ```

2. **Rows (Records or Tuples):**
   - **Definition:** Each row represents a single record in the table.
   - **Example:** A row in the "Students" table might be (1, 'John Doe', '2000-01-01').


### Normalization and its Types

**Normalization:**
- **Definition:** The process of organizing data in a database to reduce redundancy and improve data integrity.

**1NF (First Normal Form):**
- **Definition:** Ensures that each column contains atomic (indivisible) values, and each column contains values of a single type.
- **Example:** No repeating groups or arrays.
- **SQL Example:**
  ```sql
  CREATE TABLE Employees (
      EmployeeID INT PRIMARY KEY,
      Name VARCHAR(100),
      PhoneNumber VARCHAR(15) -- Each column should have atomic values
  );
  ```

**2NF (Second Normal Form):**
- **Definition:** Achieves 1NF and ensures that all non-key attributes are fully dependent on the primary key.
- **Example:** Eliminate partial dependency.
- **SQL Example:**
  ```sql
  CREATE TABLE Employees (
      EmployeeID INT PRIMARY KEY,
      Name VARCHAR(100)
  );

  CREATE TABLE EmployeeDetails (
      EmployeeID INT,
      Address VARCHAR(100),
      Salary DECIMAL(10, 2),
      FOREIGN KEY (EmployeeID) REFERENCES Employees(EmployeeID)
  );
  ```

**3NF (Third Normal Form):**
- **Definition:** Achieves 2NF and ensures that all non-key attributes are not dependent on other non-key attributes (eliminate transitive dependency).
- **Example:** Separate data into related tables.
- **SQL Example:**
  ```sql
  CREATE TABLE Employees (
      EmployeeID INT PRIMARY KEY,
      Name VARCHAR(100),
      DepartmentID INT
  );

  CREATE TABLE Departments (
      DepartmentID INT PRIMARY KEY,
      DepartmentName VARCHAR(100)
  );
  ```

### Denormalization

**Definition:**
- The process of combining normalized tables into larger tables to improve read performance, often at the expense of write performance and increased redundancy.

**Example:**
- Merging "Employees" and "Departments" tables into a single table for faster data retrieval.

**SQL Example:**
  ```sql
  CREATE TABLE EmployeeDepartments (
      EmployeeID INT,
      Name VARCHAR(100),
      DepartmentID INT,
      DepartmentName VARCHAR(100)
  );
  ```

**Example Question:** What is denormalization, and when would you use it?
- **Answer:** Denormalization is the process of merging normalized tables to improve read performance. It is used when read operations are more frequent and critical than write operations, such as in reporting systems.

### Example Interview Questions

1. **What is an RDBMS, and how does it differ from a DBMS?**
   - **Answer:** An RDBMS organizes data into tables (relations) and uses SQL for database access, supporting ACID properties for data integrity and reliability.

2. **What are the essential components of a table in a relational database?**
   - **Answer:** The essential components include columns (attributes), rows (records), primary keys, and foreign keys.

3. **Can you explain the difference between intension and extension in a database?**
   - **Answer:** Intension refers to the database schema (structure), while extension refers to the actual data stored in the database.

4. **What is normalization, and why is it important?**
   - **Answer:** Normalization is the process of organizing data to reduce redundancy and improve integrity. It is important for maintaining efficient and reliable data structures.

5. **Describe the first, second, and third normal forms with examples.**
   - **Answer:** 1NF ensures atomic values, 2NF eliminates partial dependencies, and 3NF eliminates transitive dependencies.

6. **What is functional dependency in a database?**
   - **Answer:** Functional dependency describes a relationship where one attribute uniquely determines another. It is crucial for identifying redundancy and achieving normalization.

7. **What is denormalization, and why might you use it?**
   - **Answer:** Denormalization combines normalized tables to improve read performance, used when read operations are more critical than write operations.
