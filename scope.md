### JavaScript Pillars

JavaScript has four main pillars:

1. **Scopes**
2. **Coercion and Types**
3. **Async Programming**
4. **Objects and Classes**  

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

#### Scopes in JavaScript

Scopes determine where variables or functions are organized and accessible in the code. JavaScript's scoping mechanism is different from other languages like Java, C++, and Python, so avoid mixing these concepts.

##### Types of Scope in JavaScript

1. **Global Scope**
2. **Function Scope**
3. **Block Scope**

##### 1. Global Scope

Variables declared outside any function or block are in the global scope. These variables are accessible from anywhere in your code, whether inside a function, loop, or conditional statement.

Example:
```javascript
let x = 10;

function showX() {
    console.log(x); // Accessible here
}

showX(); // Outputs: 10

console.log(x); // Accessible here too
```

In the above code, `x` is declared in the global scope, so it can be accessed both inside and outside the `showX` function.

##### 2. Function Scope

When a variable is declared inside a function, it is scoped to that function, meaning it can only be accessed within that function.

Example:
```javascript
function showY() {
    let y = 20;
    console.log(y); // Accessible here
}

showY(); // Outputs: 20

console.log(y); // Error: y is not defined
```

Here, `y` is declared inside the `showY` function, so it is only accessible within that function and not outside.

##### 3. Block Scope

Block scope is created when variables are declared inside a pair of curly braces `{}`. This can happen within loops, conditionals, or just standalone blocks.

Example:
```javascript
if (true) {
    let z = 30;
    console.log(z); // Accessible here
}

console.log(z); // Error: z is not defined
```

In this example, `z` is declared inside an `if` block, so it is only accessible within that block.

---

#### Variable Declarations and Scope

In JavaScript, variables can be declared using `var`, `let`, or `const`. The way a variable is declared affects its scope.

##### Any variable is used only in two ways:

- **RHS (Right-Hand Side):** When we consume the variable.
- **LHS (Left-Hand Side):** When we assign a value or declare the variable.

##### Lexical Scoping / Lexical Parsing:
JavaScript uses lexical scoping, also known as static scoping. In lexical scoping, the scope of variables is determined during compile time. Although variable values are assigned during the execution phase, the scope of each variable is defined during the compilation phase. Therefore, the rules for accessing variables are based on the location where functions and blocks are written in the code.

| **Scope Chaining**:
Scope chaining is the process by which JavaScript looks up variable values in the current scope and, if not found, continues searching in the outer scopes, following the chain of scopes until the variable is found or the global scope is reached. This is possible because of lexical scoping, where nested functions have access to variables in their outer functions.

Example:
```javascript
function outerFunction() {
    let outerVar = 'I am outside!';
    
    function innerFunction() {
        console.log(outerVar); // Accessible due to lexical scoping
    }
    
    innerFunction();
}

outerFunction(); // Outputs: I am outside!
```

In the above code, `innerFunction` can access `outerVar` because it is lexically within the scope of `outerFunction`. If `outerVar` were not found in the immediate scope of `innerFunction`, JavaScript would check the next outer scope (in this case, `outerFunction`'s scope) to find it, forming a chain of scopes.

In summary, **scope chaining** allows JavaScript to search through the chain of scopes to find variables, starting from the innermost scope and moving outward. This behavior is a fundamental aspect of lexical scoping..


##### **`var`:**
Variables declared with `var` are either function-scoped or globally scoped. `var` does not support block scope.

Example:
```javascript
function showVar() {
    if (true) {
        var a = 40;
    }
    console.log(a); // Accessible here, even though it's inside a block
}

showVar(); // Outputs: 40
```

**Another Example:**
```javascript
var x = 10;
console.log(x, y); // Output: 10 undefined

if (true) {
    var x = 20;
    var y = 30;
    console.log(x, y); // Output: 20 30
}

console.log(x, y); // Output: 20 30
```

In the above example, during the scope resolution phase, both `x` and `y` are declared in the global scope due to the use of `var`. When the execution phase starts:
- `x` has been initialized to `10`.
- `y` is declared in the global scope but has not been assigned a value yet, so it is `undefined`.

Within the `if` block, `x` and `y` are reassigned:
- `x` is updated to `20`.
- `y` is assigned the value `30`.

Since `var` has function or global scope, the changes to `x` and `y` in the `if` block affect their values globally. Thus, when the final `console.log(x, y);` is executed, both `x` and `y` have the values `20` and `30`, respectively.



| **Note:** _How is function scope different from block scope?_

A variable with function scope has a unique characteristic: it can be defined anywhere within the function but will still be accessible throughout the entire function.

```javascript
function fun() {
    console.log("The value of x here is", x); // The value of x here is undefined
    var x = 20;
    console.log("The value of x here is", x); // The value of x here is 20
}
```

If we try to do the same thing using `let` instead of `var`, it will result in an error because `let` does not have function scope like `var` does.



| **Note:** _Automatically Global:_  
This refers to variables that are automatically added to the global scope in certain situations. Typically, this occurs when you create a variable inside a function without using the `var`, `let`, or `const` keyword. These variables become global, even if they are defined inside a function.

```javascript
var mentor = "Ram"; // 'mentor' is declared globally

function exampleFunction() {
    mentor = "Sam"; // This modifies the global 'mentor' variable
    language = "JavaScript"; // 'language' is not declared with var/let/const, so it becomes a global variable
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


##### `let` and **`const`**: 
These keywords support block scope, meaning variables declared inside a block are only accessible within that block.
  
  Example:
  ```javascript
  function showLetConst() {
      if (true) {
          let b = 50;
          const c = 60;
          console.log(b, c); // Accessible here
      }
      console.log(b, c); // Error: b and c are not defined
  }

  showLetConst();
  ```

###### Special Characteristics of `let` and `const`

- **Block Scope Inside Functions**: Variables declared with `let` or `const` are not hoisted in the same way as `var`. They are only accessible after their declaration, which differs from the function scope provided by `var`. This difference leads to the concept of the **Temporal Dead Zone (TDZ)**.

  Example:
  ```javascript
  function checkLet() {
      console.log(x); // Error: Cannot access 'x' before initialization
      let x = 10;
  }
  
  checkLet();
  ```

  Here, `x` is in the TDZ from the start of the block until the declaration is encountered, making it inaccessible before its declaration.

- **Temporal Dead Zone (TDZ)**: This is the region of the block before the variable is declared. A variable declared with `let`, `const`, or `class` is in the TDZ from the start of the block until the code execution reaches its declaration.

- **No Redeclaration**: Variables declared with `let` and `const` cannot be redeclared in the same scope. This is enforced during the first phase (compilation phase) of the JavaScript execution process.

  Example:
  ```javascript
  let d = 70;
  let d = 80; // Error: Identifier 'd' has already been declared
  ```

---
### Hoisting

**Hoisting** is a term commonly used in the JavaScript community, although it is not officially defined in the ECMAScript specification. It refers to a behavior in JavaScript's scoping mechanism, which occurs in two main phases of code execution: the **Compilation and Scope Resolution Phase** and the **Interpretation or Execution Phase**. During the compilation phase, many variables are already identified, so when the code is executed, it seems as  JavaScript is aware of these variables or function even before their actual declaration. This phenomenon, where the interpreter appears to move the declarations of functions, variables, classes, or imports to the top of their scope before execution, is known as **hoisting**.

- **Example of Hoisting with `var` and `let`:**

```javascript
function hoist() {
    console.log(a); // undefined (var is hoisted and initialized with undefined)
    // console.log(b); // ReferenceError (let is in the Temporal Dead Zone)
    var a = 90;
    let b = 30;
    console.log(a); // 90
    console.log(b); // 30
}

hoist();
```

In this example, `var a` is hoisted, so `console.log(a);` outputs `undefined` because its value is not assigned until the line `var a = 90;`. However, `let b` is also hoisted, but it is in the **Temporal Dead Zone** (TDZ) from the start of the block until the declaration is encountered. Accessing `b` before its declaration throws a `ReferenceError` because variables declared with `let` are not initialized until the execution reaches the `let` statement. 

- **Example of Hoisting with a `Function Declaration`:**

```javascript
console.log(addNum(2, 3)); // 5

function addNum(a, b) {
    return a + b;
}
```

In this example, the function `addNum` is fully hoisted, allowing it to be called before its declaration in the code.

- **Hoisting with `Function Expressions`:**

If a function expression is created using `const` or `let`, the function itself is not available before its declaration because the variable is hoisted but remains in the **Temporal Dead Zone** (TDZ). If a function expression is created using `var`, it is hoisted but initialized with `undefined`. If you try to call the function before its definition, it will throw a `TypeError`, stating that the function is `not a function`, because the code attempts to call `undefined()`.

---
---

