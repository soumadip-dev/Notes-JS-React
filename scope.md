### JavaScript Pillars

JavaScript has four main pillars:

1. **Scopes**
2. **Coercion and Types**
3. **Async Programming**
4. **Objects and Classes**  ⭐

---

**Note:** To fully understand scoping in JavaScript, it's essential to grasp the difference between compiled and interpreted languages:

- **Compiled Languages (e.g., C, C++):** Code is analyzed and compiled into an executable binary by a compiler. Errors must be fixed before any code is executed.
- **Interpreted Languages (e.g., Bash):** Code is executed line by line. If an error occurs, execution stops at the error.
- **Hybrid Languages (e.g., Java, JavaScript, Python):** These languages use both compilation and interpretation for code execution.

---

##### Nature of JavaScript

JavaScript is a:

- **High-level:** JavaScript is a high-level language, which means it abstracts away most of the complex details of the computer, such as memory management and hardware-specific operations. Developers do not have to manage resources manually; everything happens automatically. However, this abstraction may result in lower execution speed compared to lower-level languages.
  
- **Garbage-collected:** JavaScript automatically handles memory allocation and deallocation through a process called garbage collection, which helps reduce the risk of memory leaks.
  
- **Interpreted or Just-in-Time (JIT) compiled:** JavaScript code is either interpreted by the browser or compiled just-in-time. While many believe JavaScript is purely interpreted, this isn't entirely accurate. Here's why:

  ```javascript
  console.log("wow wow"); 
  function fun() { 
    let r = uy; 
  }
  ```

  In the example above, the code throws an error without executing `console.log`, showing that JavaScript analyzes the code before starting execution.
  
- **Multi-paradigm:** JavaScript supports multiple programming paradigms, including *procedural*, *object-oriented*, and *functional programming*, offering developers flexibility in how they write code.
  
- **Prototype-based object-oriented:** JavaScript is prototype-based, meaning it uses prototypes for inheritance. Objects in JavaScript can inherit properties directly from other objects.
  
- **First-class functions:** In JavaScript, functions are first-class citizens. This means they can be treated as variables, passed into other functions, and returned from other functions.
  
- **Dynamic:** JavaScript is a dynamic language, meaning that types are determined at runtime. This offers flexibility but requires careful handling to avoid errors.
  
- **Single-threaded with an Event Loop concurrency model:** JavaScript operates in a single-threaded environment, executing one command at a time. It uses an event loop to manage concurrency, allowing it to handle asynchronous tasks without multithreading. This enables JavaScript to perform non-blocking operations and manage multiple tasks simultaneously.

---

##### Phases of Execution in JavaScript

JavaScript executes code in three distinct phases:

1. **Parsing:** This involves reading the code and converting it into a data structure called the _Abstract Syntax Tree (AST)_. This process breaks down each line of code into meaningful components for JavaScript and checks for syntax errors.
   
2. **Compilation and Scope Resolution:** In this phase, JavaScript determines the scope and visibility of each variable and function. This process is known as **scope resolution**.
   
3. **Interpretation or Execution:** During this phase, the actual execution of the code occurs, with values being assigned to variables within their respective scopes.

---

##### [Execution Context](https://youtu.be/iLWTnMzWtj4?si=mICJAs1s5TDUFHfj)

An **execution context** is an abstract concept that holds information about the environment within which the JavaScript code is executed. Every time a script or function runs, an execution context is created, determining which variables, objects, and functions are accessible during the code's execution.

###### Types of Execution Contexts:

1. **Global Execution Context:** 
   - This is the default or base context. When the JavaScript engine starts executing your code, it first creates the Global Execution Context. 
   - Variables and functions that are not inside any function are placed in the Global Execution Context.
   - There is only one Global Execution Context in any JavaScript program.
   
2. **Function Execution Context:** 
   - Every time a function is called, a new Function Execution Context is created for that function.
   - It contains the function’s own local variables, arguments object, `this` keyword, and more.
   - A Function Execution Context is created whenever a function is invoked and can be nested within other execution contexts.

3. **Eval Execution Context:** 
   - Created when `eval()` is called.
   - Generally avoided due to performance and security concerns.

###### Each execution context has two stages:

1. **Creation Phase:** 
   - Memory is allocated for variables and functions, the scope chain is established, and the `this` keyword is defined (not in arrow functions).
   - Hoisting occurs, meaning variables declared with `var` are set to `undefined`, and function declarations are loaded into memory.

2. **Execution Phase:** 
   - The code is executed line by line.
   - Values are assigned to variables, and functions are executed.

---
---
---

## Scopes in JavaScript

Scopes determine where variables or functions are organized and accessible in the code. JavaScript's scoping mechanism is different from other languages like Java, C++, and Python, so avoid mixing these concepts.

### Types of Scope in JavaScript

1. **Global Scope**
2. **Function Scope**
3. **Block Scope**

### 1. Global Scope

Variables declared outside any function or block are in the global scope. These variables are accessible from anywhere in your code, whether inside a function, loop, or conditional statement.

Example:
```javascript
let country = "India";

function showCountry() {
    console.log(country); // Accessible here
}

showCountry(); // Outputs: India

console.log(country); // Accessible here too
```

In the above code, `country` is declared in the global scope, so it can be accessed both inside and outside the `showCountry` function.

### 2. Function Scope

When a variable is declared inside a function, it is scoped to that function, meaning it can only be accessed within that function.

Example:
```javascript
function showCity() {
    let city = "Mumbai";
    console.log(city); // Accessible here
}

showCity(); // Outputs: Mumbai

console.log(city); // Error: city is not defined
```

Here, `city` is declared inside the `showCity` function, so it is only accessible within that function and not outside.

### 3. Block Scope

Block scope is created when variables are declared inside a pair of curly braces `{}`. This can happen within loops, conditionals, or just standalone blocks.

Example:
```javascript
if (true) {
    let festival = "Diwali";
    console.log(festival); // Accessible here
}

console.log(festival); // Error: festival is not defined
```

In this example, `festival` is declared inside an `if` block, so it is only accessible within that block.

---

## Variable Declarations and Scope

In JavaScript, variables can be declared using `var`, `let`, or `const`. The way a variable is declared affects its scope.

### Any variable is used only in two ways:

- **RHS (Right-Hand Side):** When we consume the variable.
- **LHS (Left-Hand Side):** When we assign a value or declare the variable.

### Lexical Scoping / Lexical Parsing
JavaScript uses lexical scoping, also known as static scoping. In lexical scoping, the scope of variables is determined during compile time. Although variable values are assigned during the execution phase, the scope of each variable is defined during the compilation phase. Therefore, the rules for accessing variables are based on the location where functions and blocks are written in the code.

| **Scope Chaining**:
Scope chaining is the process by which JavaScript looks up variable values in the current scope and, if not found, continues searching in the outer scopes, following the chain of scopes until the variable is found or the global scope is reached. This is possible because of lexical scoping, where nested functions have access to variables in their outer functions.

Example:
```javascript
function outerFunction() {
    let country = 'India';
    
    function innerFunction() {
        console.log(country); // Accessible due to lexical scoping
    }
    
    innerFunction();
}

outerFunction(); // Outputs: India
```

In the above code, `innerFunction` can access `country` because it is lexically within the scope of `outerFunction`. If `country` were not found in the immediate scope of `innerFunction`, JavaScript would check the next outer scope (in this case, `outerFunction`'s scope) to find it, forming a chain of scopes.

In summary, **scope chaining** allows JavaScript to search through the chain of scopes to find variables, starting from the innermost scope and moving outward. This behavior is a fundamental aspect of lexical scoping..

---

## `var`, `let`, and `const`

### `var`
Variables declared with `var` are either function-scoped or globally scoped. `var` does not support block scope.

**Example**:
```javascript
function showVar() {
    if (true) {
        var festival = "Diwali";
    }
    console.log(festival); // Accessible here, even though it's inside a block
}

showVar(); // Outputs: "Diwali"
```

**Another Example:**
```javascript
var city = "Mumbai";
console.log(city, state); // Output: Mumbai undefined

if (true) {
    var city = "Delhi";
    var state = "Maharashtra";
    console.log(city, state); // Output: Delhi Maharashtra
}

console.log(city, state); // Output: Delhi Maharashtra
```

In the above example, during the scope resolution phase, both `city` and `state` are declared in the global scope due to the use of `var`. When the execution phase starts:
- `city` has been initialized to `Mumbai`.
- `state` is declared in the global scope but has not been assigned a value yet, so it is `undefined`.

Within the `if` block, `city` and `state` are reassigned:
- `city` is updated to `Delhi`.
- `state` is assigned the value `Maharashtra`.

Since `var` has function or global scope, the changes to `city` and `state` in the `if` block affect their values globally. Thus, when the final `console.log(city, state);` is executed, both `city` and `state` have the values `Delhi` and `Maharashtra`, respectively.



| **Note:** _How is function scope different from block scope?_

A variable with function scope has a unique characteristic: it can be defined anywhere within the function but will still be accessible throughout the entire function.

```javascript
function electionYear() {
    console.log("Upcoming election year is", year); // undefined
    var year = 2024;
    console.log("Upcoming election year is", year); // 2024
}
```

If we try to do the same thing using `let` instead of `var`, it will result in an error because `let` does not have function scope like `var` does.


| **Note:** _Automatically Global:_  
This refers to variables that are automatically added to the global scope in certain situations. Typically, this occurs when you create a variable inside a function without using the `var`, `let`, or `const` keyword. These variables become global, even if they are defined inside a function.

```JavaScript
var primeMinister = "Narendra Modi"; // Declared globally

function updatePM() {
    primeMinister = "Indira Gandhi"; // Modifies the global variable
    currency = "Rupee"; // 'currency' is not declared with var/let/const, so it becomes a global variable
}

console.log("Current Prime Minister:", primeMinister); // Narendra Modi
// console.log("Currency:", currency); // Error (not yet defined)

updatePM(); // Call function to modify `primeMinister` and declare `currency`
console.log("Current Prime Minister:", primeMinister); // Indira Gandhi
console.log("Currency:", currency); // Rupee
```

```javascript
var mentor = "Ram"; // 'mentor' is declared globally

function exampleFunction() {
    mentor = "Sam"; // This modifies the global 'mentor' variable
    language = "JavaScript"; // 'currency' is not declared with var/let/const, so it becomes a global variable
}
console.log("Current mentor:", mentor); // Ram
// console.log("Current language:", language);  // Error because 'language' is not yet defined
exampleFunction(); // calling the function to modify mentor and declare language globally
console.log("Current mentor:", mentor); // Sam
console.log("Current language:", language); // JavaScript
```

Automatic global variables can cause issues in JavaScript. To prevent this, you can enable **strict mode** by adding the following at the top of your script:

```javascript
"use strict";
```

### `let` and `const`: 
These keywords support block scope, meaning variables declared inside a block are only accessible within that block.
  
  **Example**:

```javascript
function showLetConst() {
    if (true) {
        let state = "West Bengal";
        const capital = "Kolkata";
        console.log(state, capital); // Accessible inside the block
    }
    console.log(state, capital); // Error: `state` and `capital` are not defined outside the block
}

showLetConst();
```

#### Special Characteristics of `let` and `const`

- **Block Scope Inside Functions**: Variables declared with `let` or `const` are not hoisted in the same way as `var`. They are only accessible after their declaration, which differs from the function scope provided by `var`. This difference leads to the concept of the **Temporal Dead Zone (TDZ)**.

**Example**:
```javascript
function checkLet() {
    console.log(festival); // Error: Cannot access 'festival' before initialization
    let festival = "Holi";
}

checkLet();
```

  Here, `festival` is in the TDZ from the start of the block until the declaration is encountered, making it inaccessible before its declaration.

- **Temporal Dead Zone (TDZ)**: This is the region of the block before the variable is declared. A variable declared with `let`, `const`, or `class` is in the TDZ from the start of the block until the code execution reaches its declaration.

- **No Redeclaration**: Variables declared with `let` and `const` cannot be redeclared in the same scope. This is enforced during the first phase (compilation phase) of the JavaScript execution process.

**Example**:
```javascript
let independenceYear = 1947;
let independenceYear = 1857; // Error: Identifier 'independenceYear' has already been declared
```

---

## Closures

A `closure` provides access to the variables of its parent function even after that parent function has returned. The function keeps a reference to its outer scope, preserving the scope chain over time. This means that the variable environment of the execution context in which the function was created remains accessible even after that execution context has finished.

**Example**:
```javascript
const bookTrainTicket = function () {
    let ticketsBooked = 0;
    return function () {
        ticketsBooked++;
        console.log(`🚆 ${ticketsBooked} ticket(s) booked for Indian Railways`);
    };
};

const ticketCounter = bookTrainTicket();

ticketCounter(); // 🚆 1 ticket(s) booked for Indian Railways
ticketCounter(); // 🚆 2 ticket(s) booked for Indian Railways
ticketCounter(); // 🚆 3 ticket(s) booked for Indian Railways
```

This example demonstrates how the inner function retains access to `passengerCount`, even after `secureBooking` has completed its execution.

---

## Variable Shadowing & Illegal Shadowing
### Variable Shadowing

Variable shadowing happens when a variable in an inner scope (inside `{}`) has the same name as a variable in an outer scope. The inner variable "shadows" the outer one within its block.

**Example**:

```JavaScript
function showCapital() {
    let capital = "Delhi"; // Outer scope
    if (true) {
        let capital = "Mumbai"; // Inner scope shadows the outer variable
        console.log("Inside block:", capital); // Prints: Mumbai
    }
    console.log("Outside block:", capital); // Prints: Delhi (outer variable remains unchanged)
}

showCapital();
```
### Illegal Shadowing

Illegal shadowing happens when we try to shadow a `let` variable using `var`, which JavaScript does not allow. The reason is that `var` is function-scoped, while `let` is block-scoped. If `var` is declared inside a block, it "escapes" the block due to its function scope, causing a conflict with the existing `let` variable.

```Javascript
function festivalSeason() {
    let festival = "Diwali";
    if (true) {
        var festival = "Holi"; // ❌ Not allowed! 'var' cannot shadow 'let'
        console.log(festival);
    }
}
festivalSeason();
```

🔴 **Error:** `SyntaxError: Identifier 'festival' has already been declared`

---
## Hoisting

**Hoisting** is a term commonly used in the JavaScript community, although it is not officially defined in the ECMAScript specification. It refers to a behavior in JavaScript's scoping mechanism, which occurs in two main phases of code execution: the **Compilation and Scope Resolution Phase** and the **Interpretation or Execution Phase**. During the compilation phase, many variables are already identified, so when the code is executed, it seems as  JavaScript is aware of these variables or function even before their actual declaration. This phenomenon, where the interpreter appears to move the declarations of functions, variables, classes, or imports to the top of their scope before execution, is known as **hoisting**.

- **Example of Hoisting with `var` and `let`:**

```javascript
function hoistExample() {
    console.log(city); // undefined (var is hoisted and initialized with undefined)
    // console.log(state); // ❌ ReferenceError (let is in the Temporal Dead Zone)
    var city = "Kolkata";
    let state = "West Bengal";
    console.log(city); // Kolkata
    console.log(state); // West Bengal
}

hoistExample();
```

In this example:

- `var city` is hoisted, so `console.log(city);` outputs `undefined` because its value is not assigned until the line `var city = "Kolkata";`.
- `let state` is also hoisted, but it is in the **Temporal Dead Zone (TDZ)** from the start of the block until the declaration is encountered. Accessing `state` before its declaration throws a **ReferenceError** because variables declared with `let` are not initialized until the execution reaches the `let` statement.

- **Example of Hoisting with a `Function Declaration`:**

```javascript
console.log(getTrainFare(500, 2)); // 1000 Rupees

function getTrainFare(price, passengers) {
    return `${price * passengers} Rupees`;
}
```

In this example, the function `getTrainFare` is fully hoisted, allowing it to be called before its declaration in the code.

- **Hoisting with `Function Expressions`:**

If a function expression is created using `const` or `let`, the function itself is not available before its declaration because the variable is hoisted but remains in the **Temporal Dead Zone** (TDZ). If a function expression is created using `var`, it is hoisted but initialized with `undefined`. If you try to call the function before its definition, it will throw a `TypeError`, stating that the function is `not a function`, because the code attempts to call `undefined()`.

```JavaScript
console.log(bookFlight(3)); // TypeError: bookFlight is not a function

var bookFlight = function (seats) {
    return `✈️ ${seats} seat(s) booked for Air India`;
};
```

---
---
