#### **1. Server-Side Rendering (SSR) vs. Static Site Generation (SSG)**  

SSR (Server-Side Rendering) and SSG (Static Site Generation) are two different rendering strategies in Next.js and other frameworks:  

- **SSR (Server-Side Rendering)**:  
  - Pages are generated dynamically on each request at runtime.  
  - Useful for dynamic content that frequently updates (e.g., dashboards, authenticated pages).  
  - Improves SEO since the content is fully rendered on the server before reaching the client.  
  - Example: Using `getServerSideProps()` in Next.js.  

- **SSG (Static Site Generation)**:  
  - Pages are pre-built at build time and served as static HTML.  
  - Ideal for static content that doesn’t change often (e.g., blogs, documentation, marketing sites).  
  - Offers the best performance since pages are cached and served via a CDN.  
  - Example: Using `getStaticProps()` in Next.js.  

- **CSR (Client-Side Rendering)** : 
    - Pages are rendered on the browser after JavaScript loads.  
    - Pros: Fast navigation after initial load.  
    - Cons: Poor SEO without hydration techniques.  
    - Example: Using `useEffect()` to fetch data on mount.  

- **When to use what?**  
  - If content updates frequently → **SSR** (e.g., stock prices, live scores).  
  - If content remains mostly static → **SSG** (e.g., blog posts, landing pages). 
  - need user interaction based rendering then use **CSR**. 

---

#### **2. State Management (useState, useEffect, useContext, Redux)**  
State management in React depends on the complexity of the application:  

- **useState** → Best for local component state (e.g., form inputs, toggles).  
- **useEffect** → Handles side effects like API calls, subscriptions, and event listeners.  
- **useContext** → Provides a way to pass state globally without prop drilling, but it's limited in scalability.  
- **Redux** → Centralized state management, best for large applications where multiple components need to access shared data.

- **Example use case:**  
  - **Small projects** → `useState`, `useContext`.  
  - **Medium projects** → `useReducer`, `useContext`.  
  - **Large projects** → `Redux`.  

---

#### **3. API Integration (fetch, axios)**  

API integration in React is commonly done using **fetch** or **Axios**:  

- **fetch API** (native to JavaScript):  
  - Simple but requires additional handling for errors and timeouts.  
  - Example:  
    ```js
    useEffect(() => {
      fetch('https://api.example.com/data')
        .then(res => res.json())
        .then(data => setData(data))
        .catch(err => console.error(err));
    }, []);
    ```  

- **Axios (third-party library)**:  
  - Automatically handles JSON conversion and request cancellation.  
  - Supports request/response interceptors for authentication and logging.  
  - Example:  
    ```js
    useEffect(() => {
      axios.get('https://api.example.com/data')
        .then(response => setData(response.data))
        .catch(error => console.error(error));
    }, []);
    ```  

- **Which one to prefer?**  
  - For simple requests → **fetch**.  
  - For complex use cases (authentication, interceptors, retries) → **Axios**.  

---

#### **4. Component Lifecycle and Optimization (React.memo, useCallback, useMemo)**  
**Interviewer:** How do you optimize React components?  

**Me:**  
Optimization techniques in React include:  

- **React.memo** → Prevents unnecessary re-renders by memoizing functional components.  
  - Example:  
    ```js
    const MyComponent = React.memo(({ name }) => <div>{name}</div>);
    ```  
- **useCallback** → Memoizes functions to prevent unnecessary re-creation.  
  - Example:  
    ```js
    const handleClick = useCallback(() => {
      console.log('Clicked');
    }, []);
    ```  
- **useMemo** → Memoizes computed values to avoid expensive recalculations.  
  - Example:  
    ```js
    const filteredList = useMemo(() => list.filter(item => item.active), [list]);
    ```  
- **Best Practices:**  
  - Use `React.memo` for pure components.  
  - Use `useCallback` for event handlers passed as props.  
  - Use `useMemo` for expensive calculations.  

---

#### **5. Tailwind CSS for Styling**  
 Use Tailwind CSS because:  

- **Utility-first approach** → Styles are applied using class names instead of writing custom CSS.  
- **Faster development** → No need to write separate stylesheets.  
- **Highly customizable** → Tailwind's `theme.config.js` allows customization of colors, spacing, etc.  
- **Comparison with other frameworks:**  
  - **Bootstrap** → Component-based, but less flexible than Tailwind.  
  - **CSS-in-JS (Styled Components)** → Good for scoped styles but has runtime overhead.  
  - **SASS/SCSS** → Great for structuring large stylesheets but requires extra setup.  

- **Example of Tailwind in React:**  
  ```jsx
  <button className="bg-blue-500 text-white px-4 py-2 rounded-lg hover:bg-blue-700">
    Click Me
  </button>
  ```  
  

#### **1. How does React’s Virtual DOM work?**  
React's Virtual DOM (VDOM) is a lightweight copy of the actual DOM that helps optimize rendering and improve performance.  

- **How it works:**  
  1. When a component's state or props change, React creates a new Virtual DOM tree.  
  2. It compares the new VDOM with the previous one using a **diffing algorithm**.  
  3. React identifies changes (minimal updates) and updates only the affected parts of the real DOM (reconciliation process).  
  4. The real DOM updates efficiently, avoiding costly full re-renders.  

- **Why is it beneficial?**  
  - Faster updates compared to directly manipulating the real DOM.  
  - Reduces unnecessary reflows and repaints.  
  - Improves performance, especially for dynamic applications.  

---


#### **3. How do you optimize the performance of a React application?**

Performance optimization in React involves:  

- **1. Preventing Unnecessary Re-renders:**  
  - **Use `React.memo`** → Memoizes components to avoid unnecessary renders.  
    ```jsx
    const MemoizedComponent = React.memo(MyComponent);
    ```  
  - **Use `useCallback` for event handlers** to prevent function recreation.  
  - **Use `useMemo` for expensive calculations**.  

- **2. Efficient State Management:**  
  - Keep local state minimal in components.  
  - Use **Zustand** or **Redux** for centralized state to avoid prop drilling.  

- **3. Lazy Loading & Code Splitting:**  
  - Load components only when needed using React’s `React.lazy()`.  
  - Use dynamic imports in Next.js.  
    ```jsx
    const HeavyComponent = dynamic(() => import("./HeavyComponent"), { ssr: false });
    ```  

- **4. Optimized Image Loading:**  
  - Use **Next.js Image Component** (`next/image`) for better performance.  
  - Use lazy loading for images outside the viewport.  

- **5. Avoiding Unnecessary API Calls:**  
  - Use caching with **React Query** or SWR.  
  - Use **debouncing** in search inputs to reduce API calls.  

- **Real-world example:**  
  - In my **PMS project**, I used React.memo and lazy loading to improve dashboard performance.  

---

#### **4. How do you ensure a webpage is responsive?**  
  
Ensure responsiveness using:  

- **1. Mobile-first approach:**  
  - Start designing for smaller screens and scale up.  
- **2. Tailwind CSS for flexible styling:**  
  - Utility classes like `flex`, `grid`, `w-full`, `hidden md:block`.  
  - Example:  
    ```jsx
    <div className="p-4 md:p-8 lg:flex lg:justify-between">
      <div className="w-full lg:w-1/2">Content</div>
    </div>
    ```  
- **3. CSS Grid & Flexbox:**  
  - Use **`grid-cols-1 md:grid-cols-2`** in Tailwind to create adaptive layouts.  
- **4. Media queries (`@media`) for breakpoints:**  
  ```css
  @media (min-width: 768px) {
    .sidebar {
      display: block;
    }
  }
  ```  
- **5. Testing across devices:**  
  - Use Chrome DevTools, Lighthouse, and responsive design tools.  

- **Experience from Marketinggall Internship:**  
  - Worked on a marketing website where I optimized layouts using Tailwind.  
  - Created responsive landing pages and dynamic grids that adjusted based on screen sizes.  

---

#### **5. What’s your approach to translating mockups into code?**  
**Interviewer:** How do you approach converting a design mockup into a functional web page?  

**Me:**  
My approach includes:  

- **1. Understanding the Design:**  
  - Analyze Figma/Adobe XD mockups for layout, typography, and components.  
- **2. Setting Up a Component-Based Structure:**  
  - Break UI into reusable components (e.g., Navbar, Button, Card).  
- **3. Using Tailwind CSS for Rapid Styling:**  
  - Utility-first approach for quick responsiveness.  
  - Example:  
    ```jsx
    <button className="bg-blue-500 text-white py-2 px-4 rounded-md hover:bg-blue-700">
      Click Me
    </button>
    ```  
- **4. Implementing Dynamic Content:**  
  - Fetch data from APIs and integrate it dynamically.  
- **5. Performance Optimization:**  
  - Lazy load images, minimize CSS, and optimize rendering with `React.memo`.  
- **6. Ensuring Accessibility (a11y):**  
  - Use semantic HTML (`<button>`, `<nav>`).  
  - Add ARIA attributes where necessary.  

- **Example from My Projects:**  
  - Translated a PMS dashboard UI from Figma into a fully functional React app.  
  - Used Tailwind for styling and Zustand for state management.  

---

### **3. How do you optimize performance in a Next.js application?**  
To optimize a Next.js application, I follow these best practices:  

#### **1. Server-Side Rendering (SSR) and Static Site Generation (SSG)**
- Use **SSG (`getStaticProps`)** for pages that don’t change often to improve speed.  
- Use **SSR (`getServerSideProps`)** only when fresh data is needed per request.  

#### **2. Optimized Image Loading**
- Use **Next.js Image Optimization (`next/image`)** to serve responsive and lazy-loaded images.  
  ```jsx
  import Image from "next/image";
  <Image src="/logo.png" width={300} height={200} alt="Logo" priority />;
  ```

#### **3. Code Splitting & Lazy Loading**
- Use **dynamic imports** to load components only when needed.  
  ```jsx
  import dynamic from "next/dynamic";
  const HeavyComponent = dynamic(() => import("../components/HeavyComponent"), { ssr: false });
  ```

#### **4. API Optimization**
- Use **incremental static regeneration (ISR)** to regenerate static pages periodically.  
- Use **caching strategies** for API calls with SWR or React Query.  
  ```js
  import useSWR from 'swr';
  const { data } = useSWR('/api/posts', fetcher);
  ```

#### **5. Avoid Unnecessary Re-renders**
- Use **React.memo**, **useCallback**, and **useMemo** to optimize component rendering.  
- Use **Zustand or Redux** for efficient global state management.  

---

### **4. What is middleware in Next.js, and how do you use it?**  
Middleware in Next.js allows you to run logic **before** completing a request. It is useful for authentication, request logging, and redirects.  

#### **How to Implement Middleware:**  
Create a `_middleware.js` or `middleware.ts` file in the root directory.  

```js
import { NextResponse } from "next/server";

export function middleware(req) {
  const url = req.nextUrl.clone();
  
  // Example: Redirect if user is not authenticated
  if (!req.cookies.token && url.pathname.startsWith("/dashboard")) {
    url.pathname = "/login";
    return NextResponse.redirect(url);
  }
  
  return NextResponse.next();
}
```

**Use Cases:**  
- **Authentication:** Restrict access to pages.  
- **Redirects & Rewrites:** Redirect users dynamically.  
- **Security & Headers:** Modify request headers before processing.  

---

### **5. What is code splitting in React, and how do you implement it?**  
**Code splitting** breaks large JavaScript bundles into smaller chunks, loading only what's necessary. This improves page load times and performance.  

#### **How to Implement Code Splitting in React?**  

1. **Using React’s `React.lazy()` and `Suspense`**  
   ```jsx
   import React, { Suspense } from "react";

   const LazyComponent = React.lazy(() => import("./HeavyComponent"));

   function App() {
     return (
       <Suspense fallback={<div>Loading...</div>}>
         <LazyComponent />
       </Suspense>
     );
   }
   ```

2. **Using Next.js `dynamic()` Import for Code Splitting**  
   ```jsx
   import dynamic from "next/dynamic";
   const DynamicComponent = dynamic(() => import("../components/HeavyComponent"), { ssr: false });

   export default function Home() {
     return <DynamicComponent />;
   }
   ```

**Benefits:**  
✅ Reduces initial bundle size.  
✅ Loads components only when needed.  
✅ Improves performance for large applications.  

---

### **6. What is the difference between controlled and uncontrolled components?**  

| Feature           | Controlled Component | Uncontrolled Component |
|------------------|--------------------|----------------------|
| **State Management** | Managed by React (`useState`) | Managed by the DOM (ref) |
| **Data Handling** | React updates value (`onChange`) | Uses direct DOM access (`ref`) |
| **Use Case** | Forms with validation | Simple inputs where React control isn't needed |
| **Example** | `<input value={state} onChange={handleChange} />` | `<input ref={inputRef} />` |

#### **Example of a Controlled Component:**
```jsx
function ControlledInput() {
  const [value, setValue] = useState("");

  return (
    <input 
      type="text"
      value={value}
      onChange={(e) => setValue(e.target.value)}
    />
  );
}
```

#### **Example of an Uncontrolled Component:**
```jsx
function UncontrolledInput() {
  const inputRef = useRef(null);

  const handleSubmit = () => {
    alert(inputRef.current.value);
  };

  return (
    <>
      <input type="text" ref={inputRef} />
      <button onClick={handleSubmit}>Submit</button>
    </>
  );
}
```

**Which one to use?**  
- **Use controlled components** when you need validation, controlled state, or React forms.  
- **Use uncontrolled components** when interacting directly with the DOM is simpler.  

---