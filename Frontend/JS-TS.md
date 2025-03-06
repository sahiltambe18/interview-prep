### **JavaScript/TypeScript Concepts**  

- **Closures** → A closure is a function that remembers the variables from its outer scope even after the outer function has executed.  
  - Example:  
    ```js
    function outer() {
      let count = 0;
      return function inner() {
        count++;
        console.log(count);
      };
    }
    const counter = outer();
    counter(); // 1
    counter(); // 2
    ```  
- **Promises** → An object representing the eventual completion or failure of an asynchronous operation. It has three states: `pending`, `resolved`, and `rejected`.  
  - Example:  
    ```js
    const fetchData = () => {
      return new Promise((resolve, reject) => {
        setTimeout(() => resolve("Data received"), 2000);
      });
    };
    fetchData().then(console.log).catch(console.error);
    ```  
- **async/await** → A cleaner way to handle asynchronous operations compared to `.then()`.  
  - Example:  
    ```js
    async function getData() {
      try {
        let response = await fetch("https://api.example.com");
        let data = await response.json();
        console.log(data);
      } catch (error) {
        console.error(error);
      }
    }
    getData();
    ```  

---

#### **2. Differences Between `let`, `const`, `var`**  

- **`var`** (function-scoped, hoisted)  
  - Can be re-declared and updated.  
  - Example:  
    ```js
    var x = 10;
    var x = 20; // No error
    ```  
- **`let`** (block-scoped, not hoisted)  
  - Can be updated but not re-declared in the same scope.  
  - Example:  
    ```js
    let y = 30;
    y = 40; // Allowed
    let y = 50; // Error
    ```  
- **`const`** (block-scoped, cannot be reassigned)  
  - Used for constants.  
  - Example:  
    ```js
    const z = 100;
    z = 200; // Error
    ```  

---

#### **3. Event Loop and Asynchronous Programming**  

The **event loop** is responsible for handling asynchronous operations in JavaScript. It works as follows:  

1. **Call Stack** → Executes synchronous code first.  
2. **Web APIs** → Asynchronous tasks like `setTimeout`, `fetch` are delegated to the browser.  
3. **Callback Queue** → Once async tasks finish, their callbacks move to the queue.  
4. **Event Loop** → Moves tasks from the queue to the call stack when it's empty.  

Example:  
```js
console.log("Start");

setTimeout(() => console.log("Timeout"), 0);

Promise.resolve().then(() => console.log("Promise resolved"));

console.log("End");
```
**Output:**  
```
Start  
End  
Promise resolved  
Timeout  
```  



### **1. Implement a Debounce Function in JavaScript**  
A **debounce function** ensures that a function is called only after a specified delay has passed since the last time it was invoked. This is useful for optimizing performance in search inputs, window resizing, and API calls.  

#### **Implementation:**  
```js
function debounce(fn, delay) {
  let timer;
  return function (...args) {
    clearTimeout(timer);
    timer = setTimeout(() => fn.apply(this, args), delay);
  };
}

// Example usage:
const handleSearch = debounce((query) => {
  console.log("Fetching results for:", query);
}, 500);

handleSearch("React"); // Will execute after 500ms if no further calls occur
```
---

### **2. Implement a Throttle Function in JavaScript**  
A **throttle function** ensures that a function is called at most once in a specified interval, even if it's triggered multiple times. This is useful for optimizing scroll, resize, or button-click events.  

#### **Implementation:**  
```js
function throttle(fn, limit) {
  let lastCall = 0;
  return function (...args) {
    const now = Date.now();
    if (now - lastCall >= limit) {
      lastCall = now;
      fn.apply(this, args);
    }
  };
}

// Example usage:
const handleScroll = throttle(() => {
  console.log("User scrolled!");
}, 1000);

window.addEventListener("scroll", handleScroll);
```
---

