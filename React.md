## What is a Package Manager?

A **package manager** is a tool that automates the process of installing, updating, configuring, and managing libraries or packages for a specific programming language or platform. These packages are pre-written pieces of code or tools that developers can use to add features to their projects without having to write everything from scratch.
**Examples**:
- **npm** (The default package manager for JavaScript and Node.js. Open-source developers use `npm` to share software and tools.)
- **pip** (Python Package Installer)
- **Yarn** (An alternative to `npm` for managing JavaScript libraries)

##### How to Initialize npm?

To initialize `npm`, you can use the following commands:

```bash
npm init
```

To skip the setup step and allow `npm` to create the `package.json` file automatically without configurations, use:

```bash
npm init -y
```

---
## Bundlers in React: A Simple Overview

- A bundler combines your JavaScript, CSS, and other assets into one or a few files.
- This reduces the number of files the browser needs to load, making your application load faster.
- During development, your code remains modular, but the bundler ensures efficient delivery in production.
- By reducing the number of files, bundlers improve the efficiency of file transfers from the server to the client.
- This process helps in enhancing load times and overall performance of the application.

##### Why Do We Need a Bundler?

- **Code Splitting**: Breaks your app into smaller pieces that load only when needed, speeding up performance.
- **Dependency Management**: Combines all the required dependencies into a single bundle.
- **Optimization**: Minifies JavaScript, removes unused code (tree-shaking), and compresses assets to load faster.
- **Development Tools**: Provides features like hot module replacement (HMR) to improve the development process.
- **Efficient File Transfer**: Reduces the time taken to transfer files, making your app load faster.

##### Examples of Bundlers:

- Webpack
- Parcel
- Vite

##### Installation Commands for Parcel:

- **Install:**
    
    ```
    npm install -D parcel
    ```
    
    `-D` is used for development and as a development dependency.
    
- **Parcel Commands:**
    
    - For development build:
        
        ```
        npx parcel <entry_point>
        ```
        
    - For production build:
        
        ```
        npx parcel build <entry_point>
        ```
        
---
## What is the `.parcel-cache` folder?

The `.parcel-cache` folder (or `cache folder` in Parcel v2) stores information about your project during the build process. It helps Parcel avoid re-parsing and re-analyzing everything from scratch during rebuilds, making it faster, especially in development mode.

---
## What is `npx`?

`npx` stands for `Node Package eXecute`. It’s a tool that allows you to run any JavaScript package from the npm registry without needing to install it. `npx` comes pre-installed with npm version 5.2 and later.

---
## What is the difference between `dependencies` and `devDependencies`?

- **`dependencies`**: Packages needed for your application to run in production.
- **`devDependencies`**: Packages required only for development and testing.

---
## What is Tree Shaking in Parcel?

Tree shaking (or dead code elimination) removes unused code from your production build. By analyzing your source code, Parcel can exclude parts that aren’t being used, making your final bundle smaller and faster to load.

---
## What is Hot Module Replacement?

Hot Module Replacement (HMR) allows you to replace, add, or remove modules in your application while it’s running, without a full page reload. This helps speed up development by keeping the app state intact and only updating the changed parts.

---
## What is the difference between `package.json` and `package-lock.json` files?

- `package.json` defines project properties, such as dependencies, scripts, description, author, license, and more.
- `package-lock.json` locks dependencies to specific version numbers, ensuring consistent installations across environments.
- `package-lock.json` tracks the entire tree of dependencies (including dependencies of dependencies) and the exact version of each.
- `package-lock.json` is a generated file and is not designed to be manually edited.
- You should commit `package-lock.json` to your code repository.
- `package-lock.json` cannot be published and is ignored if found outside the root of the project.
- Avoid manually updating `package.json` to prevent breaking synchronization with `package-lock.json`.

---
## What is `node_modules`? Is it a good idea to push that on git?

The `node_modules` folder contains generated code. This is not code you've written and you should never make any updates to the files inside Node modules as it may be overwritten when installing modules.
It’s better to not commit the `node_modules` folder and add it to `.gitignore`.
Reasons not to commit:
- The folder can be very large (up to Gigabytes).
- It can be easily recreated using `package.json`.

---
## What is the `dist` folder?

The `dist` folder stands for "distributable." It contains the minified (compressed) version of your code. This is the code that is used in live, production websites.

In Parcel, the default folder for your output files is called `dist`. If you want to change the name, you can use the `--dist-dir public` tag to make the folder called `public` instead of `dist` to avoid confusion.

---
## What is `browserlists`?

**Browserslist** is a tool used to specify which browsers your project should support. It helps you define a list of supported browsers (like Chrome, Firefox, Safari, etc.) based on certain criteria, such as the most popular browsers or a specific version range.

---

## What is `^` (caret) and `~` (tilde) in `package.json`?

These are version specifiers used to define dependency versions in `package.json`:

- **`~` (Tilde):** Allows patch updates only. For example, `~1.2.3` allows versions like `1.2.4`, `1.2.5`, but not `1.3.0`.
- **`^` (Caret):** Allows minor and patch updates. For example, `^1.2.3` allows versions like `1.3.0`, `1.4.0`, but not `2.0.0`.

**Key Difference:**  
`~` is stricter, allowing only patch updates, while `^` is more flexible, permitting minor and patch updates.

---

## What are Script Types in HTML?

The `<script>` tag’s `type` attribute specifies the type of script:

1. **`type="text/javascript"` (default):** Specifies regular JavaScript. This is the default type and can be omitted.
    
    ```html
    <script type="text/javascript">
      console.log("Hello!");
    </script>
    ```
    
2. **`type="module"`:** Indicates the script is a JavaScript module, enabling ES6 features like `import` and `export`. Modules automatically run in strict mode and have module-level scope.
    
    ```html
    <script type="module">
      import { sayHello } from './module.js';
      sayHello();
    </script>
    ```
    
3. **`type="application/json"`:** Embeds JSON data into a webpage, which can be fetched or parsed with JavaScript.
    
    ```html
    <script type="application/json" id="config">
      { "theme": "dark", "lang": "en" }
    </script>
    ```
    
4. **`type="text/plain"`:** Prevents the script from being executed. Often used for embedding raw content or templates.
    
    ```html
    <script type="text/plain" id="template">
      <h1>Welcome!</h1>
    </script>
    ```

5. **`type="text/babel"`:** Indicates that the script is written using Babel, a JavaScript transpiler. Babel is required to transpile and run this script type.
    ```html
    <script type="text/babel">
      const App = () => <h1>Hello, JSX!</h1>;
    </script>
    ```

6. **`type="text/typescript"`:** Ipecifies that the script is written in TypeScript. The browser cannot execute TypeScript directly; it must be transpiled to JavaScript using a tool like the TypeScript compiler or Babel.
    ```html
    <script type="text/typescript">
      let message: string = "Hello, TypeScript!";
      console.log(message);
    </script>
    ```

**Note:** If the `type` attribute is omitted, the default script type is assumed to be JavaScript.

---
## What is `JSX`?

- JSX stands for **JavaScript XML**.
- JSX allows you to write HTML elements directly within JavaScript and insert them into the DOM without using `createElement()` or `appendChild()` methods.
- JSX simplifies the process of writing and adding HTML in React applications.
- JSX converts HTML tags into React elements.
- With JSX, you can write both the markup and logic of a component in a single `.jsx` file, making it easier to maintain and debug.

-  **Example 1: Using JSX**

```jsx
const myElement = <h1>I Love JSX!</h1>; // use () in multiline JSX
const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(myElement);
```

- **Example 2: Without JSX**

```jsx
const myElement = React.createElement('h1', {}, 'I do not use JSX!');
const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(myElement);
```

---
## Is `JSX` mandatory for React?

`JSX` is a syntax extension for JavaScript that allows you to write HTML-like code within JavaScript, making it easier to create and visualize React components. These `JSX` elements are ultimately compiled into calls to `React.createElement(component, props, ...children)`, which generate React elements that are rendered to the DOM.

While `JSX` simplifies writing React components and improves code readability, it is **not mandatory**. You can create React components and elements directly using plain JavaScript by calling `React.createElement`. However, without `JSX`, the code can become less intuitive and harder to maintain. For these reasons, most developers prefer using `JSX` to write clean and expressive React code.

---

## Is `ES6` mandatory for React?

`ES6` is not mandatory for `React` but is highly recommendable. The latest projects created on React rely a lot on ES6. React uses ES6, and you should be familiar with some of the new features like: Classes, Arrow Functions, Variables(let, const).
ES6 stands for ECMAScript 6. ECMAScript was created to standardize JavaScript, and ES6 is the 6th version of ECMAScript, it was published in 2015.

---
## What is Babel and how does it work in React?

In React, we write JSX, which looks like HTML but is not valid JavaScript syntax. Since browsers cannot understand JSX directly, it needs to be converted (or transpiled) into regular JavaScript. This is where Babel comes in.

Babel is a JavaScript transpiler that converts JSX into browser-compatible JavaScript code. It works behind the scenes when we use a bundler (like Webpack) to create a React app. The Babel setup is included in the `node_modules` folder of the React app.

In addition to transpiling JSX, Babel also converts modern JavaScript (like ES6+) into an older version of JavaScript that works in older browsers. This ensures compatibility across various browser environments.

---

## What is Component Composition?

Component Composition is a way to combine small, reusable pieces of code (called components) to build bigger and more complex parts of an application. It’s like using building blocks to create a structure. Each block does its own job, and together they make the whole thing work.

---

## What is `<React.Fragment></React.Fragment>` and `<></>`?

`<React.Fragment></React.Fragment>` is a feature in React that allows you to return multiple elements from a React component by allowing you to group a list of children without adding extra nodes to the DOM.
`<></>` is the shorthand tag for `React.Fragment`. The only difference between them is that the shorthand version does not support the key attribute.

##### Example

```jsx
return (
        <React.Fragment>
            <Header />
            <Navigation />
            <Main />
            <Footer />
        </React.Fragment>
    );

return (
        <>
            <Header />
            <Navigation />
            <Main />
            <Footer />
        </>
    );
```

---
## Props

Props are data passed from a parent component to a child component. They let the child component use this data for rendering or logic.

**Example:**

```jsx
// Parent Component
function App() {
  return <Greeting name="Soumadip" />;
}

// Child Component
function Greeting(props) {
  return <h1>Hello, {props.name}!</h1>;
}
```

**Output:**  
Hello, Soumadip!

---
## What is `Config Driven UI`?

A `Config Driven UI` is built based on the configuration data that the application receives. This approach makes the app more dynamic and easier to update. It is a common and simple way to create user interfaces that can adapt to changes.

Using a `Config Driven UI` saves development time and effort, as it provides a flexible and reusable structure. For example, a login form in most apps often requires updates, such as adding new form validations, dropdown options, or design changes. With a `Config Driven UI`, these updates can be handled easily without rewriting a lot of code.

---

## Why do we need `keys` in React?

A `key` is a special attribute you need to include when creating lists of elements in React. Keys are used in React to identify which items in the list are changed, updated, or deleted. In other words, we can say that keys are unique Identifier used to give an identity to the elements in the lists.
Keys should be given to the elements within the array to give the elements a stable identity.
##### Example

```
<li key={0}>1</li>
<li key={1}>2</li>
<li key={2}>3</li>
```

---

## Can we use `index as keys` in React?

Yes, we can use the `index as keys`, but it is not considered as a good practice to use them because if the order of items may change. This can negatively impact performance and may cause issues with component state.
Keys are taken from each object which is being rendered. There might be a possibility that if we modify the incoming data react may render them in unusual order.

---

## What is the difference between `Named export`, `Default export`, and `* as export`?

In ES6, we can export and import modules to use them in other files. There are three main ways to export modules: `Named export`, `Default export`, and `* as export`.

##### 1. Named Export

- Allows multiple named exports per file.
- When importing, the names must match exactly, and `{}` braces are required.

**Example:**  
Exporting components from `MyComponent.js`:

```jsx
export const MyComponent = () => {};
export const MyComponent2 = () => {};
```

Importing named exports:

```jsx
// Importing a single named export
import { MyComponent } from "./MyComponent";

// Importing multiple named exports
import { MyComponent, MyComponent2 } from "./MyComponent";

// Renaming an import
import { MyComponent2 as MyNewComponent } from "./MyComponent";
```

##### 2. Default Export

- Only one default export is allowed per file.
- The import name can be anything, and `{}` braces are not used.

**Example:**  
Exporting a default component from `MyComponent.js`:

```jsx
const MyComponent = () => {};
export default MyComponent;
```

Importing the default export:

```jsx
import MyComponent from "./MyComponent";
```

##### 3.` * as` Export

- Imports all the exports from a module as a single object, which allows accessing individual exports as properties.

**Example:**  
Exporting multiple components from `MyComponent.js`:

```jsx
export const MyComponent = () => {};
export const MyComponent2 = () => {};
export const MyComponent3 = () => {};
```

Importing all exports:

```jsx
import * as MainComponents from "./MyComponent";
```

Using in JSX:

```jsx
<MainComponents.MyComponent />
<MainComponents.MyComponent2 />
<MainComponents.MyComponent3 />
```

##### Combining `Named Export` and `Default Export`

You can use both export types in the same file.

**Example:**  
Exporting:

```jsx
export const MyComponent2 = () => {};
const MyComponent = () => {};
export default MyComponent;
```

Importing:

```jsx
import MyComponent, { MyComponent2 } from "./MyComponent";
```

This approach gives flexibility by allowing both named and default imports.

---

## What are `React Hooks`?

React Hooks were introduced in React 16.8. They are simple JavaScript functions that let you use reusable logic in functional components. Hooks can handle state and side effects without needing to write class components. This makes it easy to share and reuse logic across different components.

##### Common built-in React Hooks:

- **useState**: Manages state. It gives a state variable and a function to update it.
- **useEffect**: Handles side effects like API calls, timers, or subscriptions.
- **useContext**: Provides the current value of a context.
- **useReducer**: An alternative to useState for managing complex state.
- **useCallback**: Memorizes a callback function to prevent unnecessary re-renders.
- **useMemo**: Memorizes a value for better performance.
- **useRef**: Gives a mutable object to access a child component or store a value that doesn’t re-render.
- **useLayoutEffect**: Runs synchronously after DOM updates. Prefer useEffect for most cases.
- **useDebugValue**: Adds labels for custom hooks in React DevTools.

---

## What is State, and Why Do We Need It?
- **State** is a type of data that a component holds over time. It’s essential for information that a component needs to "remember" across the app's life cycle.
- Think of it as the component’s **memory**.
- **State Variable/Piece of State**: Refers to a single piece of data within a component’s state.
- Updating **component state** prompts React to **re-render the component**.
- **Examples of state** include things like notification counts, the text in an input field, or the active tab in a tabbed interface.

---

## State VS Props

| Feature               | **State**                                      | **Props**                                                             |
| --------------------- | ---------------------------------------------- | --------------------------------------------------------------------- |
| **Definition**        | Internal data managed by the component itself. | Data passed from a parent component.                                  |
| **Ownership**         | Owned by the component.                        | Owned by the parent component.                                        |
| **Modifiability**     | Can be updated within the component.           | Read-only; cannot be modified by the child component.                 |
| **Trigger Re-render** | Yes, when state is updated.                    | Yes, when new props are received (usually from parent state changes). |
| **Purpose**           | Used for interactivity and component memory.   | Used to configure child components (like function parameters).        |
| **Example Usage**     | Storing a user’s input in a form.              | Displaying text or settings from a parent component.                  |

---

## Why Do We Need the useState Hook in React? What Are Its Rules?

The `useState` hook is essential for maintaining state in a React application. It allows us to add and manage state within a functional component. The `useState` hook ensures that the UI updates dynamically whenever the state changes. When the state is updated, React re-renders the component with the new state value, keeping the UI synchronized with the underlying data.

The `useState` hook is a special function that takes the **initial state** as an **argument** and **returns an array** with two elements:
1. The current state value.
2. A function to update the state.

The `useState` hook encapsulates a single state value. To manage multiple pieces of state, you need to make separate calls to `useState`.

##### Syntax of `useState`

```jsx
const [state, setState] = useState(initialState);
```

##### Importing `useState`

To use `useState`, import it from React like this:

```jsx
import React, { useState } from "react";
```

##### Example of Using `useState` in a Functional Component

```jsx
const Example = (props) => {
  const [count, setCount] = useState(0); // Using useState

  return <div>{count}</div>;
};
```

##### Rules for Using `useState`
1. **Do not call `useState` outside a functional component** – hooks can only be used inside React functional components.
2. **Call hooks at the top level** – never call `useState` inside loops, conditions (`if-else`), or nested functions.
3. **Maintain readability** – call `useState` separately for each state variable you want to manage.

---

## What happens if we do `console.log(useState())`?

If you log `useState()` to the console, you’ll see an array: `[undefined, function]`.

- The first item (`state`) is `undefined`.
- The second item (`setState`) is a function called `dispatchSetState`.

---

## Difference between `Virtual DOM` and `Real DOM`?

DOM stands for `Document Object Model`, which represents your application UI and whenever the changes are made in the application, this DOM gets updated and the user is able to visualize the changes. DOM is an interface that allows scripts to update the content, style, and structure of the document.

##### Virtual DOM
  - Virtual DOM is a lightweight copy of the real DOM. It can be updated without directly affecting the actual DOM.
  - Think of it like a blueprint of a machine—changes are made to the blueprint but don’t immediately affect the machine.
  - **Reconciliation** is the process of comparing the Virtual DOM and Real DOM to apply only necessary updates. React uses a **diffing algorithm** for this process.
  
##### Real DOM
  - The Real DOM is a tree-like structure representing the actual web page. Developers can modify it using JavaScript.
  - Any changes to the Real DOM require re-rendering the updated elements and their children, making it slower.
  - For example, if a list is updated, the Real DOM re-renders the entire list, not just the updated part.

| `Real DOM`                                                       | `Virtual DOM`                                            |
| ---------------------------------------------------------------- | -------------------------------------------------------- |
| DOM manipulation is very expensive                               | DOM manipulation is very easy                            |
| There is too much memory wastage                                 | No memory wastage                                        |
| It updates Slow                                                  | It updates fast                                          |
| It can directly update HTML                                      | It can’t update HTML directly                            |
| Creates a new DOM for every update                               | Only updates changed elements in JSX                     |
| It allows us to directly target any specific node (HTML element) | It can produce about 200,000 Virtual DOM Nodes / Second. |
| It represents the UI of your application                         | It is only a virtual representation of the DOM           |

---

## What is `Reconciliation` in React?

- `Reconciliation` is the process that helps React update the Browser DOM efficiently.
- React uses a `diffing algorithm` to make component updates faster and more predictable.
- When a component is updated, React compares the real DOM with the Virtual DOM (a lightweight copy of the DOM).
- React keeps a copy of the real DOM called the `Virtual DOM`.
- When there are changes, React creates a new Virtual DOM and compares it with the old one using the `Diffing Algorithm`.
- React identifies which parts of the Virtual DOM have changed and updates only those parts in the real DOM.
- This process is called Reconciliation, and it makes React more efficient by updating only what is necessary.

---

## What is `React Fiber`?

React Fiber is a system in ReactJS that makes rendering faster, smoother, and smarter. It was introduced in React 16 to improve the reconciliation process. Fiber helps React handle updates more efficiently.

Since Fiber is asynchronous, React can:
- Pause, resume, and restart rendering work as new updates come in
- Reuse completed work or cancel it if not needed
- Split work into smaller parts and prioritize tasks based on importance

---

## Why is React fast?

React uses `React Fiber`, a new algorithm for `Reconciliation`. It compares the two versions of the `Virtual DOM`—the older one and the newer one. React identifies the differences (updates) between them and re-renders only the portions of the UI where updates are found, instead of re-rendering the entire page. This efficient update process makes React fast.

---

## What is `Microservice`?

`Microservice` (or microservice architecture) is a way to build software where it’s divided into small, independent parts like a database, server, or UI. These parts communicate with each other using clear APIs and are managed by small teams.

This approach makes software easier to scale, faster to build, and helps add new features quickly. Each service handles a specific task (following the **Separation of Concerns** principle) and has one clear responsibility (**Single Responsibility Principle**). This makes the system modular and easier to maintain.

##### **Benefits of Microservices**:

- Flexible Scaling
- Easy Deployment
- Freedom to Use Different Technologies
- Reusable Code
- Better Resilience

---

## What is `Monolith architecture`?

`Monolith architecture` is a traditional way of building software where everything is combined into a single, self-contained unit. All the parts of the software, like the database, server, and user interface, are tightly connected in one code base.

To make any changes, you need to update the entire system by modifying the code, rebuilding, and redeploying the application. This process can be time-consuming and restrictive because the software is not divided into smaller, independent modules.

---

## What is the difference between `Monolith and Microservice`?

|**Aspect**|**Monolithic Architecture**|**Microservices Architecture**|
|---|---|---|
|**Structure**|All processes are `tightly coupled` and run as a `single service`.|Built as `independent components` where each process runs as a `separate service`.|
|**Scaling**|The entire application must be scaled even if only one process experiences a spike in `demand`.|`Individual services` can be scaled independently based on `demand`.|
|**Complexity**|Becomes harder to `add or improve features` as the `codebase grows`.|Easier to implement `new features` as services are `focused`.|
|**Failure Impact**|`Single process failure` impacts the entire application.|`Failure` in one service doesn’t `affect others`.|
|**Communication**|Processes are `interconnected`.|Services communicate using `lightweight APIs`.|
|**Flexibility**|`Difficult` to implement `new ideas`.|More `flexible` for updates and deployments.|
|**Business Focus**|Built as one `large unit`.|Each service is `focused` on a `single function`.|

---

## `useEffect` Hook in React

The `useEffect` hook in React is used to handle side effects in functional components. Side effects include actions like **fetching API data**, **updating the DOM**, and **setting up subscriptions or timers**, which need careful handling to avoid unwanted behaviors.

##### `useEffect` takes **Two Arguments:**

- The first argument is a **callback function** that contains the side-effect logic.
- The second argument is the **dependency array** (optional), which controls when the `useEffect` should run:
    - **No dependency array**: The `useEffect` runs after every render.
    - **Empty dependency array `[]`**: The `useEffect` runs only after the first render. This is useful for tasks like fetching data after the initial page load.
    - **Non-empty dependency array `[currentState]`**: The `useEffect` runs every time any value inside the array changes. This can be used to trigger side effects when specific state or props are updated.

##### Syntax Examples:

1. **`useEffect` with an empty dependency array:**
    
    ```jsx
    useEffect(() => {
      // Side effect logic here (e.g., fetching data)
    }, []);
    ```
    
    This runs only after the first render, ideal for fetching API data.
    
2. **`useEffect` with a dependency array:**
    
    ```jsx
    useEffect(() => {
      setCurrentState("true");
    }, [currentState]);
    ```
    
    The callback runs whenever `currentState` changes.
    
3. **`useEffect` with no dependency array:**
    
    ```jsx
    useEffect(() => {
      // This runs every time the component re-renders
    });
    ```
    
    This will be triggered on every render, which could lead to unnecessary side effects if not carefully managed.
    
---

## What is `Shimmer UI`?

A `Shimmer UI` looks like the actual page design but without the real content. It helps users get an idea of how the web or mobile app will look and feel while the page is still loading. This is especially useful when a page takes more than 3–5 seconds to load, as it shows users that something is happening in the background.

Instead of displaying a loading spinner or circle, using a shimmer effect enhances the user experience by making the wait feel more interactive and visually appealing.

---

## What is `CORS`?

CORS (Cross-Origin Resource Sharing) is a system that uses HTTP headers to let a server specify which other origins (domains, schemes, or ports) can access its resources.

It provides a way for a browser and server to communicate and decide if it’s safe to allow a request from a different origin.

---
## What is `Conditional Rendering`?

`Conditional rendering` in React means showing different UI elements based on certain conditions, similar to how conditions work in `JavaScript`. You can use `if`, the `ternary operator`, or logical `&&` to decide what to display. React automatically updates the UI based on these conditions.

Here’s an example:

```jsx
// Using the Ternary Operator (shorthand for if-else)
{isLoggedIn ? <UserGreeting /> : <GuestGreeting />}

// Using an if-else statement
if (isLoggedIn) {
  return <UserGreeting />;
} else {
  return <GuestGreeting />;
}

// Using Logical AND (&&)
{isLoggedIn && <button>Logout</button>}
```

---

## Types of Routing

##### 1. Server-Side Routing (SSR)

- In server-side routing, every navigation triggers an HTTP request to the server.  
- The server processes the request and responds with a new HTML page, replacing the current one.  
- This approach is commonly used in traditional web applications.  
- **Example:** In SSR, every URL change requires a round trip to the server to fetch and display a new webpage.  

##### 2. Client-Side Routing (CSR)

- Client-side routing is managed by the browser, eliminating the need to reload the page.  
- On the initial load, the entire web application is fetched from the server and sent to the client.  
- Subsequent URL changes are handled by a router library, dynamically rendering only the required components without sending requests to the server.  
- This approach is commonly used in Single Page Applications (SPAs), such as those built with frameworks like React.  

---

## What is `SPA`?

A **Single Page Application (SPA)** is a web application that dynamically updates the webpage with data from the web server without reloading or refreshing the entire page. 

- All the HTML, CSS, and JavaScript are retrieved during the initial load.  
- Additional data or resources are loaded dynamically as needed.  
- An SPA is sometimes referred to as a **Single-Page Interface (SPI)** and uses client-side routing.  

---

## Link component in React

In React, we usually avoid using the `<a>` anchor tag for navigation within a Single Page Application (SPA). Instead, we use the `Link` component from `react-router-dom`. To use it, import it as follows:

```jsx
import { Link } from 'react-router-dom';
```

The `Link` component prevents the browser from reloading the entire page. Instead, it updates the browser's history and renders only the specific component associated with the route. This behavior helps achieve the SPA functionality, making navigation seamless without a full page reload.

Behind the scenes, the `Link` component is essentially a wrapper around the `<a>` tag, enhanced with routing functionality.

Example:

```jsx
<Link to="/path">ABC</Link>
```

---

## `useRouteError` Hook

The `useRouteError` hook is provided by React Router to access details about errors encountered during route rendering. This hook is particularly useful for creating error boundary pages.

**Syntax**: `const error = useRouteError();`

The `error` object contains properties such as `status`, `statusText`, `message`, and more, depending on the specific error that occurred. These properties can be utilized to display meaningful error messages to users.

**Example**:

```jsx
import { useRouteError } from "react-router-dom";

function ErrorPage() {
  const error = useRouteError();

  return (
    <div>
      <h1>Oops!</h1>
      <p>Something went wrong:</p>
      <p>Status: {error.status}</p>
      <p>Status Text: {error.statusText}</p>
      <p>Error Message: {error.message}</p>
    </div>
  );
}

export default ErrorPage;
```

---

## What is the purpose of the `useParams` hook in React Router DOM, and how is it used to access URL parameters?

The `useParams` hook in React Router DOM is used to access the **URL parameters** of the current route. It returns an object containing key-value pairs of the dynamic segments defined in the route.

**Example**:

```jsx
import React from "react";
import { useParams } from "react-router-dom";

const UserProfile = () => {
  const { userId } = useParams(); // Access the `userId` parameter from the URL

  return <h1>User ID: {userId}</h1>;
};

export default UserProfile;
```

**URL**:

If the route is `/user/:userId` and you navigate to `/user/123`, `useParams()` will return:

```jsx
{ userId: "123" }
```

---
---

## React Class-Based Components

Class-based components are a way of defining components in React using ES6 classes. They extend the `React.Component` class and allow the use of state and lifecycle methods.

**Syntax**:

```jsx
import React from "react";

class ExCompo extends React.Component {
  constructor(props) {
    super(props); // Required to access `this.props`
  }
  
  render() {
    return (
      <div>
        <h1>{this.props.name}</h1>
      </div>
    );
  }
}

export default ExCompo;
```

---

## Why Use `super(props)` in the Constructor?

- In ES6, when a class extends another class (e.g., `class MyComponent extends React.Component`), the subclass must call the parent class's constructor (`super()`) **before accessing `this`**. This is enforced by JavaScript.
- In React class-based components, the `constructor` of a subclass (our component) must call `super(props)` to initialize the component properly.
- If we skip `super(props)`, **React cannot initialize `this.props`** for our component, and trying to access it will result in an error because `this.props` will still be undefined within the constructor.

---

## State in Class-Based Components

##### Declaring State

State is a special object in class components to manage dynamic data.

```jsx
constructor(props) {
  super(props);
  this.state = {
    count: 0,
    name: "React",
  };
}
```

##### Accessing State

Use `this.state` to access state variables:

```jsx
render() {
  return <h1>Count: {this.state.count}</h1>;
}
```

##### Updating State

Use `this.setState()` to update state variables. React automatically re-renders the component when state changes.

```jsx
this.setState({ count: this.state.count + 1 });
```

---

## Life Cycle of Child Class in Class-Based Components

- The life cycle flow for **one child class** in class-based components is as follows:
    1. Parent Constructor
    2. Parent Render
    3. Child Constructor
    4. Child Render
    5. Child `componentDidMount`
    6. Parent `componentDidMount`
- The life cycle flow for **two child classes** in class-based components is as follows:
    1. Parent Constructor
    2. Parent Render
    3. Child 1 Constructor
    4. Child 1 Render
    5. Child 2 Constructor
    6. Child 2 Render
    7. Child 1 `componentDidMount`
    8. Child 2 `componentDidMount`
    9. Parent `componentDidMount`

(This happens because React batches the rendering of the two child components for optimization before `componentDidMount`.)

---

## Phases of Class-Based Components / Why We Call API Inside `componentDidMount()`

Class-based components in React have three primary phases: **Mounting**, **Updating**, and **Unmounting**.

##### 1. Mounting Phase (Component Initialization and DOM Insertion)

- **`constructor(props)`**: This method is called when the component is first initialized. It is used to set up the component’s initial state and bind event handlers.
- **`render()`**: The `render()` method returns the JSX that represents the component's UI. This is called when React needs to update the DOM.
- **`componentDidMount()`**: This method is called once the component has been mounted into the DOM. It is commonly used for tasks like making API calls, setting up subscriptions, or initializing third-party libraries. Since it runs after the initial render, it’s a safe place for any side effects, such as fetching data. API calls are made here because it ensures that the component is already rendered, preventing any errors related to accessing the DOM before it's fully available.

Example:

```jsx
async componentDidMount() {
  const data = await fetch("https://api.example.com/data");
  const json = await data.json();
  this.setState({ data: json });
}
```

##### 2. Updating Phase (State or Props Change)

- **`render()`**: This method is re-invoked every time the state or props change, ensuring that the UI is updated with the new data. In the case of an API call, it triggers a re-render because the state is updated with the fetched API data (JSON).
- **`componentDidUpdate(prevProps, prevState)`**: This lifecycle method is called after the component has updated due to a change in either state or props. It's useful for responding to changes, like making additional API calls or updating state based on the new props.

Example:

```jsx
componentDidUpdate(prevProps, prevState) {
  if (prevState.count !== this.state.count) {
    console.log("Count updated!");
  }
}
```

##### 3. Unmounting Phase (Component Removal from DOM)

- **`componentWillUnmount()`**: This method is called just before the component is removed from the DOM. It is used to clean up any resources, such as clearing timers, canceling API requests, or removing event listeners. For example, when we switch to another page in a Single Page Application (SPA), components can keep running in the background even after we leave the page. If we don't stop these processes, they can slow down the browser, especially if we revisit the page and new processes start.

Example:

```jsx
componentWillUnmount() {
  clearInterval(this.timer);
}
```

For further reference, you can explore the [React Lifecycle Methods Diagram](https://projects.wojtekmaj.pl/react-lifecycle-methods-diagram/).

##### Note:

Class-based components use lifecycle methods like `componentDidMount()`, `componentDidUpdate()`, and `componentWillUnmount()`. In functional components, the same behavior is achieved using the `useEffect()` hook:

```jsx
useEffect(() => {
  // ComponentDidMount or ComponentDidUpdate logic
  return () => {
    // ComponentWillUnmount logic
  };
}, [dependencies]);
```

---
---

## Reusing Logic with Custom Hooks

Custom hooks in React are a great way to **reuse logic** across multiple components. When you find yourself writing similar code in different components, extracting that logic into a custom hook helps keep your code DRY (Don't Repeat Yourself) and maintainable.

##### Steps to Create a Custom Hook

1. **Identify reusable logic** in your components, such as fetching data, handling form input, or managing global state.
2. Extract this logic into a function that starts with the prefix `use` (e.g., `useFetchData`, `useForm`).
3. Use React hooks (like `useState`, `useEffect`, `useContext`) inside the custom hook.
4. Return the necessary values or functions from the hook so they can be used in components.

##### Example: Custom Hook for Fetching Data

Here’s an example of a custom hook for fetching data from an API.

##### 1. Create the custom hook: `useFetch.js`

```jsx
import { useState, useEffect } from "react";

const useFetch = (url) => {
  const [data, setData] = useState(null);

  useEffect(() => {
    fetchData(); // Fetch menu when component mounts
  }, []);

  const fetchData = async () => {
    const response = await fetch(url);
    const data = await response.json();
    setData(data);
  };

  return data;
};

export default useFetch;
```

##### 2. Use the custom hook in a component:

```jsx
import React from "react";
import useFetch from "./useFetch";

const UserList = () => {
  const data = useFetch("https://jsonplaceholder.typicode.com/users");
  
  return (
    <ul>
      {data && data.map((user) => (
        <li key={user.id}>{user.name}</li>
      ))}
    </ul>
  );
};

export default UserList;
```

##### Benefits of Custom Hooks

- **Reusability**: You can reuse the `useFetch` hook across multiple components without duplicating code.
- **Separation of Concerns**: Logic is moved out of components, making them cleaner and focused on presentation.
- **Testability**: You can test custom hooks independently of components.

---

## Lazy loading

Lazy loading in React is a technique used to load components only when they are needed, rather than loading everything upfront when the app starts. This helps improve performance by reducing the initial load time, which can be especially useful for larger applications with many components.

In React, lazy loading is implemented using `React.lazy()` in combination with `Suspense`. Here's how it works:

##### Steps for Lazy Loading:

1. **Use `React.lazy()`**: This is used to dynamically import a component only when it's required.

    Example:
    ```jsx
    const MyComponent = React.lazy(() => import('./MyComponent'));
    ```
    
2. **Wrap the component in `Suspense`**: Since lazy-loaded components can take some time to load, React provides `Suspense` to handle this loading state. You can display a loading spinner or any other fallback UI while the component is loading.
    
    Example:
    ```jsx
    import React, { Suspense } from 'react';
    
    const MyComponent = React.lazy(() => import('./MyComponent'));
    
    function App() {
      return (
        <div>
          <Suspense fallback={<div>Loading...</div>}>
            <MyComponent />
          </Suspense>
        </div>
      );
    }
    ```
    
##### Why Use Lazy Loading:

- **Improved Performance**: Reduces the initial bundle size by loading components only when they are needed.
- **Faster Page Load**: Initially loads only essential components, improving the initial loading speed.
- **Efficient Resource Use**: Loads resources (components) only when they are required, which optimizes the use of bandwidth and memory.

Lazy loading is particularly helpful for applications with large or complex UIs, as it ensures that not all components are loaded at once, which can lead to faster render times and better user experience.


---
---
