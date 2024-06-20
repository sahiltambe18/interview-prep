### Data, Database, and File System

**Data:**
- **Definition:** Raw facts and figures that have no meaning on their own. Data can be anything like numbers, text, images, videos, etc.
- **Example:** 'John', '28', 'Engineer' are pieces of data.

**Database:**
- **Definition:** A structured collection of data, data is stored as records, typically stored and accessed from a computer system.
- **Example:** A customer database might contain data such as names, addresses, and purchase history.

**File System:**
- **Definition:** A operating system uses file sysytem to store data in files.
- **Example:** Files and folders on a computer's hard drive.

### Types of Database

1. **Relational Database:**
   - Uses tables to store data.
   - Example: MySQL, PostgreSQL.

2. **NoSQL Database:**
   - Used for large sets of unstructured data. Examples include document stores, key-value stores, wide-column stores, and graph databases.
   - Example: MongoDB, Cassandra.

3. **Hierarchical Database:**
   - Data is organized in a tree-like structure.
   - Example: IBM Information Management System (IMS).

4. **Network Database:**
   - Data is organized in a graph structure, allowing many-to-many relationships.
   - Example: Integrated Data Store (IDS).

5. **Object-oriented Database:**
   - Data is stored in the form of objects, similar to object-oriented programming.
   - Example: db4o, ObjectDB.

### What is DBMS and its Applications

**DBMS (Database Management System):**
- **Definition:** Software that uses a standard method of cataloging, retrieving, and running queries on data. DBMS manages the data, the database engine, and the database schema.
- **Applications:** Banking (transaction management), Airlines (reservations and schedules), Universities (student information), Telecommunication (call records, billing), and Online Shopping (inventory, sales).

### Need, Advantages, and Disadvantages of DBMS

**Need for DBMS:**
- To manage large amounts of data efficiently.
- To support data integrity and security.
- To facilitate concurrent access by multiple users.
- To ensure data consistency and reduce data redundancy.

**Advantages of DBMS:**
- **Data Redundancy Control:** Minimizes duplicate data.
- **Data Integrity:** Ensures accuracy and consistency of data.
- **Data Security:** Restricts unauthorized access.
- **Concurrent Access:** Allows multiple users to access data simultaneously.
- **Backup and Recovery:** Simplifies data backup and restoration.

**Disadvantages of DBMS:**
- **Complexity:** Requires sophisticated software and hardware.
- **Cost:** High initial investment and ongoing maintenance costs.
- **Performance:** Can be slower for simple operations due to the complexity of DBMS.
- **Size:** Requires substantial memory and storage.

### Data Abstraction

**Definition:**
- The process of hiding the complexities of the database from the user and showing only the necessary details.

**Levels of Data Abstraction:**
1. **Physical Level:** Describes how data is stored.
2. **Logical Level:** Describes what data is stored and the relationships among the data.
3. **View Level:** Describes only part of the entire database, tailored for a particular group of users.

### DBMS Architecture

**Definition:**
- The design of a DBMS in terms of components and their interactions.

**Types:**
1. **1-tier Architecture:** The database and the DBMS are on the same machine.
2. **2-tier Architecture:** The DBMS is on the server, and the application is on the client.
3. **3-tier Architecture:** Adds a middle layer for business logic between the client and the server.

### 2-tier Architecture

**Definition:**
- A client-server architecture where the user interface is on the client side and the database is stored on the server side.

**Components:**
1. **Client:** User interface, runs application logic.
2. **Server:** Hosts the database, processes client requests, and sends responses.

**Advantages:**
- Simpler to implement and manage.
- Direct communication between client and server.

**Disadvantages:**
- Scalability issues as the number of clients increases.
- Limited flexibility and security.

### 3-tier Architecture

**Definition:**
- An architecture that includes three layers: the presentation layer (client), the application layer (business logic), and the data layer (database server).

**Components:**
1. **Presentation Layer:** User interface (UI).
2. **Application Layer:** Business logic and processing.
3. **Data Layer:** Database and data management.

**Advantages:**
- Enhanced scalability and flexibility.
- Better security as the business logic is separate from the database.
- Easier maintenance and updates.

**Disadvantages:**
- More complex to implement.
- Increased latency due to additional layer.
- Higher cost due to the need for additional infrastructure.

