## **1. Difference Between Process and Thread in Node.js**
In Node.js, **processes** and **threads** are distinct execution units:

| Feature           | Process                           | Thread                             |
|------------------|--------------------------------|--------------------------------|
| **Definition**    | An instance of a program running independently. | A lightweight execution unit within a process. |
| **Memory**       | Each process has its own memory space. | Threads within the same process share memory. |
| **Communication** | Processes communicate via IPC (Inter-Process Communication). | Threads share memory, making communication faster but riskier (due to race conditions). |
| **Node.js Usage** | Handled using `child_process` module. | Handled using the `worker_threads` module. |
| **Concurrency**   | Processes are independent and can run in parallel. | Threads run concurrently but share the same process space. |

### **When to Use**
- Use **processes** for CPU-intensive tasks (e.g., data processing, image manipulation).
- Use **threads** for tasks that require shared memory or frequent communication.

---

## **2. Difference Between Child Processes and Worker Threads**
Node.js supports both **child processes** and **worker threads** for parallel execution, but they serve different purposes.

| Feature            | Child Process (`child_process`)         | Worker Thread (`worker_threads`) |
|-------------------|----------------------------------|----------------------------------|
| **Memory Usage**  | Each child process has its own memory space. | Threads share memory with the parent process. |
| **Performance**   | Higher overhead due to separate memory. | Lower overhead due to shared memory. |
| **Communication** | Uses IPC (message passing). | Uses `SharedArrayBuffer` for fast communication. |
| **Use Case**      | Best for CPU-intensive tasks and running separate applications. | Best for performance-heavy tasks that need shared memory. |
| **Scaling**      | More expensive in terms of memory. | More efficient for large-scale applications. |

### **Example**
- Use **child processes** when running external scripts or executing commands.
- Use **worker threads** for parallel computations like cryptographic operations.

---

## **3. Purpose of `process.env` in Node.js**
`process.env` is an object that stores **environment variables** in Node.js. These variables are key-value pairs accessible within the runtime.

### **Why Use `process.env`?**
1. **Configuration Management** – Store API keys, database credentials, and service URLs.
2. **Security** – Keeps sensitive data out of source code.
3. **Portability** – Easily switch between environments (development, staging, production).

### **Example Usage**
```javascript
// Set an environment variable in terminal:
// export DB_HOST=127.0.0.1 (Linux/macOS)
// set DB_HOST=127.0.0.1 (Windows)

console.log(process.env.DB_HOST); // Output: 127.0.0.1
```

### **Best Practices**
- Use a `.env` file and `dotenv` package:
```javascript
require('dotenv').config();
console.log(process.env.DB_HOST);
```
- Never commit `.env` files to version control (`.gitignore` them).

---

## **4. How Does Node.js Prevent Blocking Operations?**
Node.js is single-threaded but **non-blocking**, meaning it prevents operations from blocking the event loop using:

### **1. Asynchronous I/O**
- Uses the **libuv** library for non-blocking I/O operations.
- Example: Reading a file asynchronously.
```javascript
const fs = require('fs');
fs.readFile('file.txt', 'utf8', (err, data) => {
    if (err) throw err;
    console.log(data);
});
console.log('File read requested'); // Runs before file reading completes
```

### **2. Event Loop**
- Handles asynchronous callbacks using the **Reactor Pattern**.
- Delegates long-running tasks to the OS or worker threads.

### **3. Callbacks, Promises, and Async/Await**
- Example: Non-blocking database query using promises.
```javascript
async function fetchData() {
    let data = await db.query("SELECT * FROM users");
    console.log(data);
}
fetchData();
```

### **4. Worker Threads and Child Processes**
- Offload CPU-heavy tasks to avoid blocking the main thread.

---

## **5. Purpose of `async_hooks` in Node.js**
The `async_hooks` module in Node.js allows tracking asynchronous operations.

### **Use Cases**
- Debugging async operations.
- Profiling and performance monitoring.
- Implementing a custom logging system.

### **Example: Tracking Async Operations**
```javascript
const async_hooks = require('async_hooks');

const hook = async_hooks.createHook({
    init(asyncId, type, triggerAsyncId) {
        console.log(`Async operation started: ${type}, ID: ${asyncId}`);
    },
    destroy(asyncId) {
        console.log(`Async operation completed: ID: ${asyncId}`);
    }
});
hook.enable();

// Example async function
setTimeout(() => console.log("Async task done"), 1000);
```

---

## **6. How Would You Optimize the Performance of a Node.js Application?**  
Optimizing a Node.js application involves multiple strategies, including efficient resource utilization, proper architecture, and caching.

### **1. Use Asynchronous Code Efficiently**
- Avoid blocking the **event loop** with CPU-intensive tasks.
- Use **Promises** or **Async/Await** instead of callbacks.
```javascript
async function fetchData() {
    const data = await db.query("SELECT * FROM users");
    console.log(data);
}
```

### **2. Use Clustering and Load Balancing**
- Node.js runs on a **single thread**, so using **clustering** can distribute workloads.
- Example using `cluster`:
```javascript
const cluster = require('cluster');
const http = require('http');
const numCPUs = require('os').cpus().length;

if (cluster.isMaster) {
    for (let i = 0; i < numCPUs; i++) {
        cluster.fork();
    }
} else {
    http.createServer((req, res) => {
        res.writeHead(200);
        res.end('Hello World!');
    }).listen(8000);
}
```

### **3. Implement Caching (Redis)**
- Reduce **database load** by caching frequently used data.
```javascript
const redis = require('redis');
const client = redis.createClient();

client.set("key", "value");
client.get("key", (err, reply) => {
    console.log(reply);
});
```

### **4. Optimize Database Queries**
- Use **indexes** in SQL.
- Use **pagination** to limit data retrieval.
- Use **connection pooling**.

### **5. Compress Responses & Enable Gzip**
```javascript
const compression = require('compression');
app.use(compression());
```

### **6. Use PM2 for Process Management**
- Automatically restart services on failure.
```bash
pm2 start server.js --name "my-app"
```

---

## **7. Explain How WebSockets Work in Node.js**
WebSockets allow **real-time** communication between clients and servers.

### **How It Works**
1. **Client establishes a WebSocket connection** with the server.
2. **A persistent, full-duplex connection** is created.
3. **Both client and server can send/receive messages asynchronously.**

### **Example using `ws` library**
#### **Server-side WebSocket**
```javascript
const WebSocket = require('ws');
const server = new WebSocket.Server({ port: 8080 });

server.on('connection', ws => {
    ws.send('Welcome!');
    ws.on('message', message => {
        console.log(`Received: ${message}`);
        ws.send(`Echo: ${message}`);
    });
});
```
#### **Client-side WebSocket**
```javascript
const socket = new WebSocket('ws://localhost:8080');

socket.onmessage = (event) => {
    console.log(`Server: ${event.data}`);
};

socket.onopen = () => {
    socket.send('Hello Server!');
};
```

---

## **8. How Do You Implement Caching in a Node.js Application (Redis)?**
### **Why Use Caching?**
- **Speeds up response time.**
- **Reduces load on databases.**

### **Implementation with Redis**
1. Install Redis & the Node.js package:
```bash
npm install redis
```

2. **Connect to Redis**
```javascript
const redis = require('redis');
const client = redis.createClient();

client.on('connect', () => {
    console.log('Connected to Redis');
});
```

3. **Cache API Responses**
```javascript
const fetchData = async (req, res) => {
    const key = 'users';

    client.get(key, async (err, data) => {
        if (data) {
            return res.json(JSON.parse(data)); // Return cached data
        }

        const users = await db.query('SELECT * FROM users');
        client.setex(key, 3600, JSON.stringify(users)); // Cache data for 1 hour
        res.json(users);
    });
};
```

---

## **9. How Do You Implement a Rate Limiter in Node.js?**
A **rate limiter** prevents excessive requests to a server.

### **Using `express-rate-limit`**
1. Install package:
```bash
npm install express-rate-limit
```

2. **Configure Rate Limiter**
```javascript
const rateLimit = require('express-rate-limit');

const limiter = rateLimit({
    windowMs: 1 * 60 * 1000, // 1 minute
    max: 10, // Limit each IP to 10 requests per window
    message: "Too many requests, please try again later.",
});

app.use(limiter);
```

---

## **10. Explain the Reactor Pattern and How It Relates to Node.js**
The **Reactor Pattern** is a design pattern used for **handling multiple concurrent requests efficiently**. It’s the core of **Node.js’s event-driven, non-blocking architecture**.

### **How It Works**
1. **Event Loop:** Listens for events and schedules tasks.
2. **Non-blocking I/O:** Uses callbacks instead of waiting.
3. **Worker Pool:** Offloads CPU-intensive tasks.

### **Example**
```javascript
const fs = require('fs');

fs.readFile('file.txt', 'utf8', (err, data) => {
    console.log(data);
});

console.log('File read requested'); // Runs before file reading completes
```
Here, the **event loop** registers the readFile operation and moves on, preventing blocking.

---

## **11. Difference Between `fork()`, `spawn()`, and `exec()` in `child_process` Module**
Node.js allows creating child processes for parallel execution.

| Function  | Description | When to Use |
|-----------|------------|-------------|
| `spawn()` | Launches a new process, streaming output. | Continuous data processing (e.g., streaming). |
| `exec()`  | Runs a command and buffers output. | Short commands with small outputs. |
| `fork()`  | Creates a new Node.js instance. | Running separate Node.js scripts. |

### **Example Usage**
#### **1. `spawn()` - Streaming Output**
```javascript
const { spawn } = require('child_process');

const ls = spawn('ls', ['-lh']);
ls.stdout.on('data', data => console.log(`Output: ${data}`));
```

#### **2. `exec()` - Buffering Output**
```javascript
const { exec } = require('child_process');

exec('ls -lh', (err, stdout, stderr) => {
    console.log(`Output: ${stdout}`);
});
```

#### **3. `fork()` - Running a Separate Script**
```javascript
const { fork } = require('child_process');

const child = fork('child.js');
child.send('Hello');
child.on('message', msg => console.log(`Message from child: ${msg}`));
```

---
