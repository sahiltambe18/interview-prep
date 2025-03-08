## **1. What is Node.js, and how does it work? How does it differ from traditional server-side technologies like PHP or Java?**  
**Node.js** is a **runtime environment** that allows you to run JavaScript on the server. It is built on Google’s **V8 JavaScript engine** and uses an **event-driven, non-blocking I/O model**, making it lightweight and efficient for scalable applications.  

### **Differences from PHP & Java:**  
| Feature        | Node.js                     | PHP                      | Java                      |
|---------------|----------------------------|--------------------------|---------------------------|
| **Execution**  | Non-blocking, event-driven | Blocking (traditional)    | Multi-threaded, blocking  |
| **Concurrency** | Single-threaded, async I/O | Multi-threaded (Apache) | Multi-threaded JVM       |
| **Performance** | Faster (non-blocking I/O) | Slower for high requests | High performance          |
| **Use Case**   | Real-time apps, APIs      | Web apps, CMS           | Enterprise applications   |
| **Syntax**    | JavaScript-based           | PHP (procedural/OOP)     | Java (strict OOP)         |

---

## **2. What are the advantages of using Node.js?**
- **Asynchronous & Non-Blocking**: Handles multiple requests without waiting for previous ones to complete.  
- **Single Programming Language**: Uses JavaScript on both frontend & backend.  
- **Fast Execution**: Uses V8 engine to compile JS directly to machine code.  
- **Scalability**: Event-driven architecture makes it easy to scale horizontally.  
- **Rich Package Ecosystem**: **npm** provides thousands of reusable libraries.  
- **Real-Time Applications**: Ideal for WebSockets, chat apps, streaming services.  

---

## **3. Explain the event-driven architecture of Node.js.**
Node.js is **event-driven**, meaning it **listens for events** and executes callback functions when those events occur.  

Example:
```js
const EventEmitter = require("events");
const myEmitter = new EventEmitter();

myEmitter.on("userLoggedIn", (user) => {
  console.log(`${user} has logged in.`);
});

myEmitter.emit("userLoggedIn", "John");
```
Here, `on()` registers an event listener, and `emit()` triggers the event.

---

## **4. What is the difference between synchronous and asynchronous programming in Node.js?**
| Type          | Synchronous (Blocking)   | Asynchronous (Non-Blocking) |
|--------------|--------------------------|-----------------------------|
| **Execution** | Executes one task at a time | Executes multiple tasks concurrently |
| **Performance** | Slower, waits for each task to finish | Faster, doesn't block execution |
| **Use Case** | Suitable for CPU-intensive tasks | Best for I/O operations (DB, network requests) |

### **Example:**
**Synchronous (Blocking)**
```js
const fs = require("fs");
const data = fs.readFileSync("file.txt", "utf8");
console.log(data);
```

**Asynchronous (Non-Blocking)**
```js
fs.readFile("file.txt", "utf8", (err, data) => {
  if (err) throw err;
  console.log(data);
});
```
In asynchronous mode, the program continues execution while waiting for the file read operation.

---

## **5. What is the difference between CommonJS and ES modules in Node.js?**
| Feature         | CommonJS (`require`) | ES Modules (`import`) |
|---------------|----------------------|-----------------------|
| **Default in Node.js** | Yes (before ES6) | No (introduced in ES6) |
| **Syntax** | `const x = require('x')` | `import x from 'x'` |
| **File Extension** | `.js` | `.mjs` (or enable `"type": "module"` in `package.json`) |
| **Usage** | Works synchronously | Works asynchronously |

**CommonJS Example:**
```js
const fs = require("fs");
module.exports = { myFunction };
```

**ES Module Example:**
```js
import fs from "fs";
export const myFunction = () => {};
```

---

## **6. How does Node.js handle concurrency?**
Node.js uses the **event loop** and **asynchronous I/O operations** to handle concurrency efficiently.

- **Single-threaded event loop**: Handles multiple requests using a single thread.
- **Asynchronous non-blocking operations**: Uses **callbacks, Promises, and async/await** for concurrent execution.
- **Worker threads (for CPU-intensive tasks)**: Uses `worker_threads` module.

Example of concurrency:
```js
setTimeout(() => console.log("Task 1"), 1000);
setTimeout(() => console.log("Task 2"), 500);
console.log("Task 3");

// Output:
// Task 3
// Task 2
// Task 1
```
---

## **7. Explain the role of the V8 engine in Node.js.**
The **V8 engine** is Google’s open-source JavaScript engine that compiles JS code directly to machine code.

### **Role in Node.js:**
- **Executes JavaScript outside the browser**.
- **Optimizes performance** using techniques like **JIT (Just-In-Time) compilation**.
- **Memory management & garbage collection**.

Example:  
```js
console.log("Hello, Node.js!");
```
Here, the V8 engine converts JS code into efficient machine code at runtime.

---

## **8. What is an event loop, and how does it work in Node.js?**
The **event loop** allows Node.js to handle **non-blocking** operations despite being single-threaded.

### **How it Works:**
1. Executes the **call stack**.
2. Handles **asynchronous operations** (setTimeout, I/O, Promises).
3. Uses **libuv** to delegate tasks to OS threads.
4. Moves completed tasks back to the **event queue**.

Example:
```js
console.log("Start");

setTimeout(() => console.log("Timeout"), 0);

console.log("End");

// Output:
// Start
// End
// Timeout
```
---

## **9. What are streams in Node.js, and how do they work?**
Streams are **efficient ways to handle large data** in chunks instead of loading it all at once.

### **Types of Streams:**
1. **Readable** – For reading data (e.g., file input).
2. **Writable** – For writing data (e.g., file output).
3. **Duplex** – Both readable & writable (e.g., sockets).
4. **Transform** – Modify data (e.g., compression).

Example (Reading file using stream):
```js
const fs = require("fs");
const stream = fs.createReadStream("file.txt", "utf8");

stream.on("data", (chunk) => console.log(chunk));
```

---

## **10. What is npm, and how does it work?**
**npm (Node Package Manager)** is used to install, manage, and publish Node.js packages.

### **Commands:**
- `npm init -y` → Initializes `package.json`
- `npm install express` → Installs Express.js
- `npm install -g nodemon` → Installs globally
- `npm update` → Updates dependencies

---

## **11. What is the role of the package.json file in a Node.js project?**
The `package.json` file:
- Stores **project metadata** (name, version).
- Manages **dependencies**.
- Defines **scripts** for automation.

Example:
```json
{
  "name": "myproject",
  "version": "1.0.0",
  "dependencies": {
    "express": "^4.17.1"
  },
  "scripts": {
    "start": "node index.js"
  }
}
```

---

## **12. What is the difference between process.nextTick() and setTimeout()?**
| Feature | `process.nextTick()` | `setTimeout()` |
|---------|----------------------|----------------|
| **Execution Order** | Runs before next event loop cycle | Runs after at least specified delay |
| **Use Case** | Used for immediate execution of callbacks | Used for delayed execution |

### **Example:**
```js
console.log("Start");

process.nextTick(() => console.log("Next Tick"));

setTimeout(() => console.log("Timeout"), 0);

console.log("End");

// Output:
// Start
// End
// Next Tick
// Timeout
```


---

## **2. What is middleware in Express.js?**  
Middleware functions in **Express.js** are functions that **execute between the request and response cycle**.

### **Types of Middleware:**
1. **Application-Level**: `app.use()`
2. **Router-Level**: `router.use()`
3. **Built-in**: `express.json()`, `express.static()`
4. **Error-Handling**: `(err, req, res, next) => {}`
5. **Third-Party**: `cors`, `helmet`, `morgan`

### **Example:**
```js
const express = require("express");
const app = express();

// Middleware function
app.use((req, res, next) => {
  console.log(`Request received: ${req.method} ${req.url}`);
  next(); // Move to next middleware
});

app.get("/", (req, res) => {
  res.send("Hello, World!");
});

app.listen(3000, () => console.log("Server running on port 3000"));
```
---

## **3. How does Node.js handle file operations (`fs` module)?**  
The `fs` (File System) module provides methods for file handling in **synchronous** and **asynchronous** ways.

### **Reading a file:**
```js
const fs = require("fs");

// Asynchronous
fs.readFile("file.txt", "utf8", (err, data) => {
  if (err) throw err;
  console.log(data);
});

// Synchronous
const data = fs.readFileSync("file.txt", "utf8");
console.log(data);
```
---

## **4. What are buffers in Node.js?**  
A **buffer** is a temporary storage area for **binary data** used in file operations, network requests, and streams.

### **Example:**
```js
const buffer = Buffer.from("Hello");
console.log(buffer); // <Buffer 48 65 6c 6c 6f>
console.log(buffer.toString()); // Hello
```
---


## **7. How do you handle errors in Node.js?**  
### **1. Try-Catch (For synchronous code):**
```js
try {
  throw new Error("Something went wrong");
} catch (err) {
  console.error(err.message);
}
```
### **2. Callback Error Handling:**
```js
fs.readFile("file.txt", "utf8", (err, data) => {
  if (err) return console.error("Error:", err);
  console.log(data);
});
```
### **3. Using Express.js Error Middleware:**
```js
app.use((err, req, res, next) => {
  res.status(500).send({ error: err.message });
});
```
---

## **8. What is the difference between synchronous and asynchronous code in Node.js? Provide an example.**  
| Feature | Synchronous (Blocking) | Asynchronous (Non-Blocking) |
|---------|----------------------|------------------|
| Execution | Line-by-line, waits for completion | Does not wait, executes next task |
| Performance | Slower, blocks execution | Faster, continues execution |

### **Example:**
```js
// Synchronous
const data = fs.readFileSync("file.txt", "utf8");
console.log(data);

// Asynchronous
fs.readFile("file.txt", "utf8", (err, data) => console.log(data));
```
---

## **12. How would you debug a Node.js application?**  
### **1. Using console.log():**
```js
console.log("Debugging data:", data);
```
### **2. Using the Node.js Debugger:**
```sh
node --inspect index.js
```
### **3. Using Chrome DevTools:**
1. Run `node --inspect-brk index.js`
2. Open Chrome DevTools (`chrome://inspect`)

---

## **13. What is the difference between `npm install` and `npm ci`?**  
| Feature | `npm install` | `npm ci` |
|---------|--------------|----------|
| **Usage** | Installs dependencies | Installs exact dependencies from `package-lock.json` |
| **Speed** | Slower | Faster |
| **Modifies package-lock.json?** | Yes | No |
| **Use Case** | Regular development | CI/CD environments |

---

### **1. What is the purpose of the cluster module in Node.js?**  

Node.js is **single-threaded** and runs on a single **CPU core** by default, meaning it cannot take full advantage of multi-core processors. The **cluster module** allows us to create multiple child processes (workers) that share the same **server port** and handle requests in parallel.

#### **Why Use Clustering?**
- Utilizes **multi-core CPUs** for better performance.
- Prevents the entire application from crashing if one worker fails.
- Distributes incoming requests among worker processes.

#### **How It Works:**
The `cluster` module uses **forking** to create child processes. Each worker runs a **copy** of the main application but shares the same server port.

#### **Example of Using Clustering in Node.js**
```js
const cluster = require("cluster");
const http = require("http");
const os = require("os");

if (cluster.isMaster) {
  console.log(`Master process ${process.pid} is running`);

  // Fork workers equal to the number of CPU cores
  for (let i = 0; i < os.cpus().length; i++) {
    cluster.fork();
  }

  // If a worker dies, restart it
  cluster.on("exit", (worker, code, signal) => {
    console.log(`Worker ${worker.process.pid} died. Starting a new one...`);
    cluster.fork();
  });
} else {
  // Worker processes run the HTTP server
  http.createServer((req, res) => {
    res.writeHead(200);
    res.end("Hello from Worker " + process.pid);
  }).listen(3000);

  console.log(`Worker ${process.pid} started`);
}
```

#### **Key Points:**
- **`cluster.isMaster`**: Determines if the process is the main (master) process.
- **`cluster.fork()`**: Creates child processes (workers).
- **Workers share the same server port**, allowing load balancing.
- If a worker **crashes**, a new worker is spawned.

#### **When to Use Clustering?**
- When handling high traffic **HTTP servers**.
- Applications needing **fault tolerance** (one worker crash doesn’t crash the whole app).
- Running CPU-intensive tasks in separate workers.

---

### **2. How does Node.js handle memory management and garbage collection?**  

#### **Memory Management in Node.js**
Memory in Node.js is managed using the **V8 JavaScript Engine**, which provides:
1. **Heap Memory** – Stores objects and closures.
2. **Stack Memory** – Stores function calls and primitive values.
3. **Buffers** – Used for handling binary data.

#### **Garbage Collection in Node.js**
V8 uses **automatic garbage collection** to free up memory that is no longer needed. It follows the **Mark-and-Sweep Algorithm**:

- **Mark Phase**: Identifies objects still in use (reachable).
- **Sweep Phase**: Cleans up unreferenced objects, reclaiming memory.

#### **Memory Optimization Tips:**
1. **Avoid Memory Leaks**:  
   - Remove event listeners (`removeListener`).
   - Clear intervals and timeouts (`clearInterval`, `clearTimeout`).
   - Close unused database connections.

2. **Use Streams Instead of Buffers**  
   **Bad Example (Buffering entire file in memory):**
   ```js
   const fs = require("fs");
   const data = fs.readFileSync("largeFile.txt", "utf8"); // High memory usage
   console.log(data);
   ```
   **Optimized Example (Streaming file data):**
   ```js
   const fs = require("fs");
   const stream = fs.createReadStream("largeFile.txt", "utf8");
   stream.on("data", (chunk) => console.log(chunk)); // Memory-efficient
   ```

3. **Monitor Memory Usage**
   ```js
   console.log(process.memoryUsage());
   ```
   This logs memory usage stats like heap used, heap total, external memory, etc.

#### **Tools for Debugging Memory Issues**
- **Node.js Heap Snapshots**: Use `node --inspect` to analyze memory.
- **Chrome DevTools**: Attach debugger to check memory leaks.

---

### **3. Explain how async/await works in Node.js. How is it different from Promises?**  

#### **What is `async/await`?**
- `async/await` is a syntactic feature built on top of Promises that makes asynchronous code **look synchronous**.
- It improves **readability** and **error handling** compared to `.then()` and `.catch()` in Promises.

#### **How `async/await` Works**
- An `async` function **always returns a Promise**.
- Inside an `async` function, the `await` keyword **pauses execution** until the Promise resolves.

#### **Example of `async/await`**
```js
function fetchData() {
  return new Promise((resolve) => {
    setTimeout(() => resolve("Data received"), 2000);
  });
}

async function getData() {
  console.log("Fetching...");
  const data = await fetchData(); // Execution pauses here until resolved
  console.log(data);
}

getData();
console.log("End of script"); // This runs while waiting for fetchData
```
**Output:**
```
Fetching...
End of script
(Data appears after 2 seconds)
Data received
```

#### **Difference Between `async/await` and Promises**
| Feature            | Promises (`.then()/.catch()`) | `async/await` |
|--------------------|--------------------------|--------------|
| Readability       | Harder with multiple `.then()` | Easier, looks synchronous |
| Error Handling    | Requires `.catch()` for errors | Uses `try/catch` |
| Chaining          | Uses `.then().then()` | Uses `await` inside `async` |
| Execution Flow    | Nested callbacks can happen | More linear execution |

#### **Error Handling in `async/await`**
```js
async function fetchData() {
  try {
    const response = await someAsyncFunction();
    console.log(response);
  } catch (error) {
    console.error("Error occurred:", error);
  }
}
```

#### **When to Use `async/await`?**
- When dealing with multiple asynchronous tasks.
- When you want **cleaner, readable** asynchronous code.
- When you need **better error handling**.

---

### **4. How does Node.js handle concurrency, given that it’s single-threaded?**  

#### **Understanding Node.js Concurrency**
- Node.js uses a **single-threaded event loop**.
- It **delegates** time-consuming operations (I/O, database, network) to **libuv**, which manages them using **worker threads**.
- This makes Node.js highly **efficient** for handling **multiple concurrent** requests.

#### **Event Loop Handling of Concurrency**
Node.js uses **asynchronous callbacks** and **non-blocking I/O** to manage concurrency.

##### **Example of Non-Blocking I/O**
```js
const fs = require("fs");

console.log("Start");

fs.readFile("file.txt", "utf8", (err, data) => {
  if (err) throw err;
  console.log("File read complete");
});

console.log("End");
```
**Output:**
```
Start
End
File read complete
```
- The file is read **asynchronously**, and execution **continues** without waiting.

#### **Worker Threads (For CPU-Intensive Tasks)**
For heavy computations, Node.js provides **worker threads**:
```js
const { Worker } = require("worker_threads");

if (require.main === module) {
  const worker = new Worker(__filename);
  worker.on("message", (msg) => console.log(msg));
  worker.postMessage("Start work");
} else {
  parentPort.postMessage("Task Done");
}
```
- This offloads CPU-intensive tasks to another thread **without blocking** the event loop.

#### **When is Node.js Good for Concurrency?**
✅ **I/O-heavy applications** (APIs, WebSockets, File Handling)  
❌ **CPU-heavy tasks** (Image processing, video encoding) → Use Worker Threads

---

### **Conclusion**
1. **Cluster Module**: Enables multi-core utilization by forking multiple processes.
2. **Memory Management**: V8 manages memory using Garbage Collection, Mark-and-Sweep algorithm.
3. **Async/Await**: Simplifies async programming, improving readability.
4. **Concurrency**: Node.js handles multiple requests via the Event Loop and Worker Threads.
