# React Hooks & React Router Essentials

## 1️⃣ useState Hook

`useState` is a React Hook used to **add state to functional components**. State lets a component **remember values** (like counters, form inputs, toggles) and **re-render** when they change.

### Syntax

```jsx
const [state, setState] = useState(initialValue);
```

* `state` → current value
* `setState` → function to update the value
* `initialValue` → starting value of the state

### Example (Counter)

```jsx
import { useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <button onClick={() => setCount(count + 1)}>
      Clicked {count} times
    </button>
  );
}
```

### ❌ Common Mistake

```jsx
<button onClick={setCount(count + 1)}></button> // Executes immediately
```

### ✅ Correct Usage

```jsx
<button onClick={() => setCount(count + 1)}></button>
```

![useState Example](/photos/usestate.jpeg)

---

## 2️⃣ useEffect Hook

`useEffect` is a React Hook used to handle **side effects**.

> A **side effect** is something that happens **as a consequence of another action**, outside the normal rendering process.

Examples of side effects:

* Fetching data from an API
* Updating `document.title`
* Setting timers (`setTimeout`, `setInterval`)
* Subscribing to events

### Syntax

```jsx
useEffect(() => {
  // side-effect code
}, [dependencies]);
```

* `setup` → code that runs after render
* `dependencies` → controls when the effect runs

### Example: Sync with Browser (Document Title)

```jsx
import { useState, useEffect } from 'react';

function App() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    document.title = `Count: ${count}`;
  }, [count]);

  return (
    <button onClick={() => setCount(count + 1)}>
      Clicked {count} times
    </button>
  );
}
```

![useEffect Example](/photos/useeffect.png)

---

### What is an API?

**API** stands for **Application Programming Interface**.

> In simple terms, an API is a set of rules and tools that allows different software applications to communicate with each other.

🔗 It acts like a **bridge between two programs**.

Examples:

* Frontend (React) requesting data from Backend (Node/Express)
* Browser fetching data from a server

---
## 4️⃣ Side Effects & API Basics

### What is a Side Effect?

A **side effect** is something that happens **as a consequence of another action**, but is **outside the normal rendering flow** of React.

Examples of side effects:

* Fetching data from an API
* Updating `document.title`
* Setting timers
* Accessing browser APIs

📌 In React, side effects are handled using **`useEffect`**.


---

## 3️⃣ useEffect with API Call Example

```jsx
import { useState, useEffect } from 'react';
import './App.css';

function App() {
  const [datas, setDatas] = useState([]);

  useEffect(() => {
    fetch("https://jsonplaceholder.typicode.com/posts")
      .then(res => res.json())
      .then((data) => setDatas(data));
  }, []);

  return (
    <ul>
      {datas.map(data => (
        <li key={data.userId}>{data.title}</li>
      ))}
    </ul>
  );
}

export default App;
```

![useEffect API Example](/photos/api.png)

---


## 5️⃣ useRef Hook

`useRef` is a React Hook used to **reference a value that does NOT cause re-rendering** when it changes.

> `useRef` is used for values that are **not needed for rendering**.

### Key Points

* Stores a **mutable value**
* Value persists between renders
* **Does NOT trigger re-render** when updated
* Similar to state, but without UI updates

### Syntax

```jsx
const ref = useRef(initialValue);
```

---

### useRef vs useState

| Feature       | useState | useRef |
| ------------- | -------- | ------ |
| Re-render     | Yes      | No     |
| Used for UI   | Yes      | No     |
| Mutable       | No       | Yes    |
| Persist value | Yes      | Yes    |

---

### Example: useState vs useRef

```jsx
import { useState, useEffect, useRef } from "react";

function App() {
  const [count, setCount] = useState(0);
  const countRef = useRef(0);
  
  const handleIncrement = () => {
    setCount(count + 1);
    countRef.current++;
    console.log("Count:", count);
    console.log("RefCount:", countRef.current);
  };

  return (
    <div>
      <h1>{countRef.current}</h1>
      <button onClick={handleIncrement}>Increment</button>
    </div>
  );
}

export default App;
```

### Explanation

* `useState` → updates UI and re-renders component
* `useRef` → updates value **without re-rendering**
* `countRef.current` changes but UI updates only when state changes

---

## 6️⃣ React Router DOM

### What is React Router DOM?

**React Router DOM** is a library used in React to handle **client-side routing**.

> Routing means navigating between different pages **without reloading the browser**.

It allows us to build **Single Page Applications (SPA)**.

---

### How Routing Works in Normal HTML

```html
<a href="/about">About</a>
```

* Browser sends a request to the server
* Whole page reloads ❌

---

### How Routing Works in React

* Page does **NOT reload**
* Only the required component changes
* Faster and smoother user experience ✅

---

### Installing React Router DOM

```bash
npm install react-router-dom
```

---

### Core Components of React Router DOM

| Component       | Purpose                      |
| --------------- | ---------------------------- |
| `BrowserRouter` | Wraps the entire app         |
| `Routes`        | Container for routes         |
| `Route`         | Defines a path and component |
| `Link`          | Navigation without reload    |
| `useParams`     | Access URL parameters        |
| `useNavigate`   | Programmatic navigation      |

---

### Basic Routing Example

```jsx
import { BrowserRouter, Routes, Route } from "react-router-dom";

function Home() {
  return <h2>Home Page</h2>;
}

function About() {
  return <h2>About Page</h2>;
}

function App() {
  return (
    <BrowserRouter>
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/about" element={<About />} />
      </Routes>
    </BrowserRouter>
  );
}

export default App;
```

---

### Navigation using Link

```jsx
import { Link } from "react-router-dom";

function Navbar() {
  return (
    <nav>
      <Link to="/">Home</Link>
      <Link to="/about">About</Link>
    </nav>
  );
}
```

✔ No page reload
✔ Faster navigation

---

### Dynamic Routing (URL Params)

```jsx
import { useParams } from "react-router-dom";

function User() {
  const { id } = useParams();
  return <h2>User ID: {id}</h2>;
}

// Route
<Route path="/user/:id" element={<User />} />
```

---

![examplle](/photos/route.png)
![examplle](/photos/useparams.png)
---
### Navigation

```jsx
import { useNavigate } from "react-router-dom";

function Login() {
  const navigate = useNavigate();

  const handleLogin = () => {
    navigate("/");
  };

  return <button onClick={handleLogin}>Login</button>;
}
```

---

### React Router DOM vs Traditional Routing

| Feature         | HTML Routing | React Router DOM |
| --------------- | ------------ | ---------------- |
| Page Reload     | Yes ❌        | No ✅           |
| Speed           | Slow         | Fast             |
| User Experience | Poor         | Smooth           |

---
# Tailwind CSS

## What is Tailwind CSS?
**Tailwind CSS** is a **utility-first CSS framework** that allows you to style elements directly in HTML or JSX using predefined utility classes.

---

## Utility Concept
Instead of writing custom CSS:
```css
.button {
  background-color: blue;
  color: white;
  padding: 8px 16px;
}
```
You use utility classes:
```css
<button class="bg-blue-500 text-white px-4 py-2 rounded">
  Click me
</button>
```
### Advantages of Tailwind CSS

1. Faster UI development
2. No need to write custom CSS
3. Highly customizable
4. Consistent design system
5. Great for React, Vite, Next.js

[Tailwinds CSS](https://tailwindcss.com)

# shadcn/ui

## What is shadcn/ui?
**shadcn/ui** is a collection of **reusable, accessible UI components** built using  
**Radix UI** and **Tailwind CSS**.

> It is not a component library you install — you **copy components into your project**.

---

## Why use shadcn/ui?
- Accessible by default (ARIA support)
- Fully customizable
- Uses Tailwind CSS
- Built on Radix UI
- Perfect for React, Vite, Next.js

---