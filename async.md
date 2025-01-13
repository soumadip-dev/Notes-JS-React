### Synchronous and Asynchronous Programming

- In synchronous programming, tasks are executed one after another, and each task must complete before the next one begins. This is the default behavior of JavaScript.
- In asynchronous programming, tasks can be initiated without waiting for previous tasks to complete. This allows for more efficient execution, especially in tasks that involve waiting, like network requests or timers.

### What is the Default Nature of JavaScript?

JavaScript is **synchronous by default**. This means that any native JavaScript code executes line by line, with each line needing to complete before the next one can begin. This synchronous nature is due to JavaScript being single-threaded.

### Example of Asynchronous Code

```javascript
setTimeout(function f() {
  console.log("Hello");
}, 3000);

console.log("End");
```

In this example, `setTimeout` is a higher-order function that delays the execution of `console.log("Hello")` by 3000 milliseconds (3 seconds). However, the code after `setTimeout`, `console.log("End");`, executes immediately.

**Important Points**:

- `setTimeout` is not a native JavaScript function; it is provided by the runtime environment (e.g., Node.js, Deno, or web browsers like Chrome, Edge, etc.).
- Similarly, `console.log()` is also provided by the runtime environment, not by JavaScript itself.
- If you pass `0` as the delay time in `setTimeout`, `Node.js` automatically sets it to 1 millisecond. Setting a delay of `0` is not actually possible in `Node.js`.

---

### How Does JavaScript Handle Runtime Code?

JavaScript manages runtime code using the **event loop** and **queues** (like the macro task queue and micro task queue). Here's a simplified explanation:

1. **Call Stack**: JavaScript has a call stack where it keeps track of the function calls. If a task in the code is related to the runtime environment (like `setTimeout`), JavaScript sends it to the runtime environment and moves on to the next line of code.
2. **Event Loop**: The event loop continuously checks if the call stack is empty. If the call stack is empty and there are tasks waiting in the queue (like a completed `setTimeout`), the event loop moves the task from the queue to the call stack for execution.
3. **Queues**: If a runtime task completes while the call stack is not empty, the runtime environment places the completed tasks into the `Macro-task queue`. The tasks in these queues are processed in a **First-Come, First-Served (FCFS)** order when the call stack is empty.

In summary, the event loop ensures that tasks are executed efficiently, even when asynchronous operations are involved.

---

### Higher-Order Functions and Callbacks

A `higher-order function` is a function that either takes another function as an argument, returns a new function, or both. The function used as an argument is called a `callback` function. By using higher-order functions, we can achieve a higher level of abstraction in our code, making it more modular and reusable.

```javascript
const radius = [1, 2];
const area = function (radius) {
    return Math.PI * radius * radius;
};
const circumference = function (radius) {
    return 2 * Math.PI * radius;
};
const calculate = function (radius, logic) {
    const output = [];
    for (let i = 0; i < radius.length; i++) {
        output.push(logic(radius[i]));
    }
    return output;
};

console.log(calculate(radius, area)); // [3.141592653589793, 12.566370614359172]
console.log(calculate(radius, circumference)); // [6.283185307179586, 12.566370614359172]
```

- `map` is also a higher-order function in arrays. Instead of `calculate`, we can use the `map` function:

```javascript
console.log(radius.map(area)); // [3.141592653589793, 12.566370614359172]
```

---

### Data Transformation with `map()`, `filter()`, and `reduce()`

JavaScript provides powerful array methods for transforming and processing data, with three key methods being `map()`, `filter()`, and `reduce()`. These methods enable efficient and readable manipulation of arrays.

### Example Array:
```javascript
const numbers = [1, 2, 3, 4, 5];
```

### 1. **`map()`**: 
Applies a given function to each element of an array, returning a new array with the transformed values.
```javascript
const doubled = numbers.map(n => n * 2); // [2, 4, 6, 8, 10]
```

### 2. **`filter()`**: 
Creates a new array containing only the elements that satisfy the provided condition.
```javascript
const greaterThanTwo = numbers.filter(n => n > 2); // [3, 4, 5]
```

### 3. **`reduce()`**: 
Executes a reducer function (that you provide) on each element of the array, resulting in a single output value. Here, `acc` is the accumulator and `r` is the current value. `r` represents each value in the array, and `acc` represents the final result. The second argument of the `reduce` function is the initial value of `acc`.

```javascript
const sum = numbers.reduce((acc, n) => acc + n, 0); // 15
```

---

### Problem with Callbacks

While callbacks are powerful and allow us to write modular, reusable code, they can sometimes lead to issues when used extensively. There are two main problems with callbacks:

1. **Inversion of Control**: 
   When we pass a callback function to another function, we give up control over when and how that callback is executed. The function receiving the callback may call it immediately, later, multiple times, or not at all. This can sometimes lead to unexpected behavior and make debugging more challenging.

2. **Callback Hell** (also known as **Pyramid of Doom**): 
   When callbacks are nested within other callbacks, especially for asynchronous operations, it can lead to deeply nested code that is difficult to read and maintain. This "pyramid" shape can make code harder to follow and increase the risk of errors.
   
   Here's an example of callback hell:
   ```javascript
   doFirstTask(() => {
       doSecondTask(() => {
           doThirdTask(() => {
               doFourthTask(() => {
                   // Final task
               });
           });
       });
   });
   ```

---

### Closures

A `closure` provides access to the variables of its parent function even after that parent function has returned. The function keeps a reference to its outer scope, preserving the scope chain over time. This means that the variable environment of the execution context in which the function was created remains accessible even after that execution context has finished.

**Example**:
```javascript
const secureBooking = function() {
    let passengerCount = 0;
    return function() {
        passengerCount++;
        console.log(`${passengerCount} passengers`);
    };
};

const booker = secureBooking();

booker(); // 1 passengers
booker(); // 2 passengers
booker(); // 3 passengers
```

This example demonstrates how the inner function retains access to `passengerCount`, even after `secureBooking` has completed its execution.

---

### What are Promises?

- Promises provide a significant improvement over callbacks, offering a more structured and readable way to manage asynchronous operations.
- A Promise is an object that represents the eventual completion (or failure) of an asynchronous task.
- They are special JavaScript objects designed to handle operations expected to complete in the future, such as data fetching or setting a timer.

**Focus Points**:
1. `How to create a promise.`
2. `How to consume a promise.`

---

### How to Create a Promise

- In JavaScript, a promise can be created using the `Promise` constructor. To do this, you call `Promise` with the `new` keyword and pass in a required parameter, resulting in a promise object.
- This constructor accepts a callback function as an argument, known as the `executor callback`.
- It is called the `executor callback` because it is executed immediately by the `Promise` constructor when the promise object is created.
- Our responsibility is to define this `callback` function, which handles the asynchronous task. The `Promise` constructor takes responsibility for executing this callback.
- The callback function accepts two parameters: `resolve` and `reject`, which are functions provided by the `Promise` constructor.

```javascript
new Promise((resolve, reject) => {
  // resolve -> resolver, reject -> rejecter
});
```

- Since the `Promise` constructor is responsible for executing the callback, it also provides the `resolve` and `reject` functions that you can define within the callback to handle the success or failure of the asynchronous task.

---

### What Does a Promise Object Look Like?

A promise object contains:

- **Status**: The current state of the promise.
- **Value**: The result of the promise.
- **OnfulFillment** [Hidden]
- **OnRejected** [Hidden]

#### Promise Status

A promise object can be in one of three states:

1. **Pending**: The initial state when the promise is created.
2. **Fulfilled**: The state when the operation inside the promise has completed successfully.
3. **Rejected**: The state when the operation inside the promise has failed.

- When a promise is created, it starts in the **pending** state.
- It transitions to either the **fulfilled** state (if `resolve` is called) or the **rejected** state (if `reject` is called).
- The transition from pending to fulfilled or rejected happens only once. Once a promise changes state, it cannot change again.

#### Promise Value

The promise object also contains a value, referred to as the "promise result." This value holds the outcome of the operation performed within the promise:

- If the promise is **fulfilled**, the value is the result of the successful operation.
- If the promise is **rejected**, the value is the error or reason for the failure.

#### Example of a Promise

```javascript
const pr = new Promise((resolve, reject) => {
  setTimeout(() => {
    const randomNum = Math.floor(Math.random() * 100);
    console.log(randomNum);

    if (randomNum % 2 === 0) {
      resolve(randomNum);
    } else {
      reject(randomNum);
    }
  }, 5000);
});

console.log(pr);
```

**Output:**
```
Promise {<pending>}

// After 5 seconds
13 (random)
Promise {<rejected>: 13}
```

#### OnFulfillment and OnRejected

- These are internal arrays managed by the promise object, initially empty.
- Functions can be stored in these arrays using the `.then()` or `.catch()` methods on the promise object.
- If the promise is in the **pending** state, the functions remain in their respective arrays.
- When the promise transitions to the **fulfilled** state, all functions in the `OnFulfillment` array are queued in the **Microtask queue**, while the `OnRejected` array does nothing.
- When the promise transitions to the **rejected** state, all functions in the `OnRejected` array are queued in the **Microtask queue**, while the `OnFulfillment` array does nothing.

---

### How to Consume a Promise

- Promises act as a placeholder object for something that will be available in the future.
- Once the future execution is done, we might want to execute some code based on the outcome.
- **Using `.then()` to Handle Promises**  
  To execute code after a promise is resolved or rejected, we can use the `.then()` method. This method takes two arguments:
  1. `onFulfillment`: A function to handle the success of the promise (required).
  2. `onRejected`: A function to handle the failure of the promise (optional).

```javascript
const pr = new Promise((resolve, reject) => {
  // Your code here
});

pr.then(onFulfillmentFunction, onRejectedFunction); 
// --> onFulfillmentFunction goes to the OnFulfillment array 
// --> onRejectedFunction goes to the OnRejected array
```

#### Promise Resolution Process
- If the promise is fulfilled (successful), the functions passed as `onFulfillment` are executed.
- If the promise is rejected (failed), the functions passed as `onRejected` are executed.
- If there are any tasks waiting in the runtime environment, they will be stored in the **macrotask queue**.
- Functions related to the promise's outcome (either success or failure) are stored in the **microtask queue**.
- The **microtask queue** has higher priority, so it runs before the **macro-task queue** once the call stack is empty.

- **Example Code**  
  Here's an example to illustrate how promises work in conjunction with other asynchronous code:

```javascript
// Create a promise that resolves after 500 ms
const promiseOne = new Promise(function executor1(resolve, reject) {
  console.log('Executor callback triggered by Promise constructor: promiseOne');
  
  setTimeout(function c1() {
    console.log('Timer of promiseOne done');
    resolve(100); // pending -> fulfilled; undefined -> 100
  }, 500);
});

// Handling the resolved or rejected value of promiseOne
promiseOne.then(
  function onSuccess() {
    console.log('onSuccess');
  },
  function onFailure() {
    console.log('onFailure');
  }
);

// Timer callback function for a separate 2-second timer
setTimeout(function timerCallback() {
  console.log('Timer 1 done');
}, 2000); // Timer of 2 seconds

// Create another promise that resolves or rejects based on a random number
const promiseTwo = new Promise(function executor2(resolve, reject) {
  console.log('Executor callback triggered by Promise constructor: promiseTwo');
  
  setTimeout(function promiseCallback() {
    const randomNumber = Math.floor(Math.random() * 100);
    console.log(randomNumber);
    
    if (randomNumber % 2 === 0) {
      resolve(randomNumber); // even number, resolve promise
    } else {
      reject(randomNumber); // odd number, reject promise
    }
  }, 3000);
});

// Handling the resolved or rejected value of promiseTwo
promiseTwo.then(
  function onSuccess(value) {
    console.log('Executing onSuccess for promiseTwo:', value);
  },
  function onFailure(value) {
    console.log('Executing onFailure for promiseTwo:', value);
  }
);

// Long-running synchronous task (not recommended in practice)
for (let i = 0; i < 1000000000; i++) {}
 
```

#### Output:
```
Execution Start
Executor callback triggered by Promise constructor: promiseOne
Executor callback triggered by Promise constructor: promiseTwo
Timer of promiseOne done
onSuccess
Timer 1 done
86
Executing onSuccess for promiseTwo: 86
```

#### Explanation:

In this code, we can observe the following sequence of events:

- **promiseOne** is created by invoking the Promise constructor, which calls the `executor1` callback. It logs "Executor callback triggered by Promise constructor: promiseOne" (Output -> 1).
- A 500 ms timer is set for the `c1` callback. Since nothing else remains in `executor1`, it is removed from the call stack.
- The status of **promiseOne** is now "Pending," and its value is `undefined`.
- The `.then()` callbacks are registered for **promiseOne**:  
  - The `onSuccess` function is added to the fulfillment array of **promiseOne**.
  - The `onFailure` function is added to the rejection array of **promiseOne**.
- A separate 2-second timer is set to trigger `timerCallback` after 2000 ms.
- **promiseTwo** is created by calling a new Promise constructor, which is added to the call stack and invokes the `executor2` callback. It logs "Executor callback triggered by Promise constructor: promiseTwo" (Output -> 2).
- A 3-second timer is set for `promiseCallback`, which will either resolve or reject **promiseTwo** based on a random number. Since there is nothing more to do in the `executor2` callback, it is removed from the call stack.
- The status of **promiseTwo** is now "Pending," and its value is `undefined`.
- The `.then()` callbacks are registered for **promiseTwo**:  
  - The `onSuccess` function is added to the fulfillment array of **promiseTwo**.
  - The `onFailure` function is added to the rejection array of **promiseTwo**.
- A long loop runs for 1 billion iterations, blocking the event loop.
- In the background, the timer function for **promiseOne** completes first, adding `c1` to the macrotask queue. This is followed by the second timer adding `timerCallback`, and finally, the timer for **promiseTwo** completes, adding `promiseCallback` to the macrotask queue.
- After some time, the loop finishes, and the call stack becomes empty.
- The event loop checks if there is anything in the microtask queue. If none is found, it checks the macrotask queue. It finds the `c1` callback, moves it to the call stack, and executes it.
- `c1` first logs "Timer of promiseOne done" (Output -> 3) and resolves **promiseOne** with a value of 100. Now, the status of **promiseOne** is "fulfilled," and the `onSuccess` function from the fulfillment array is shifted to the microtask queue. After that, `c1` is removed from the call stack.
- The event loop now finds tasks in both the microtask and macrotask queues, but it prioritizes the microtask queue over the macrotask queue.
- It takes the `onSuccess` function from the microtask queue and executes it, logging "onSuccess" (Output -> 4).
- With nothing left in the microtask queue, the event loop checks the macrotask queue, finds `timerCallback`, and executes it, logging "Timer 1 done" (Output -> 5).
- It then finds `promiseCallback` in the macrotask queue and executes it. It first generates a random number and logs it:
  `randomnum` (Output -> 6).  
  Then it resolves or rejects the promise based on the random number.
  - If the random number is even, it resolves the promise and shifts the `onSuccess` function from the fulfillment array to the microtask queue, executing it and logging: "Executing onSuccess for promiseTwo: randomnum" (Output -> 7).
  - If the number is odd, it rejects the promise and logs: "Executing onFailure for promiseTwo: randomnum" (Output -> 7).

---

### More on the `.then()` Function

- **Behaviour of `.then()` Function:**  
  The `.then()` function returns a new promise, which is different from the original promise on which it was called.

  ```javascript
  const p1 = new Promise((res, rej) => {
    setTimeout(() => {
      res("p1 resolved");
    }, 2000);
  });

  const p2 = p1.then(
    function f() {
      return "Function F";
    },
    function g() {
      console.log("Function G");
    }
  );
  ```

  **Explanation:**  
  - When `p1.then()` returns a new promise `p2`, initially, `p2` behaves like any other promise, with a value of `undefined` and a status of `pending`.
  - The resolution or rejection of `p2` is handled by the functions `f()` or `g()` provided inside the `.then()` function.
  - When `f()` or `g()` returns something, the status of `p2` will be `fulfilled`, and the return value is set to the value of `p2`.
  - If `f()` throws an exception, the status of `p2` will be `rejected`.
  - If another promise is returned from the function `f()`, then the resolution or rejection of `p2` will be dependent on the outcome of that returned promise. 
    - If the returned promise is fulfilled, `p2` will also be fulfilled with the same value.
    - If the returned promise is rejected, `p2` will be rejected with the same reason.

---

### **Chaining Promises** and **exception handling:**  
  `.then()` can be chained to handle a sequence of asynchronous operations, where the result of one operation is passed to the next. Each `.then()` in the chain returns a new promise, allowing for sequential asynchronous processing.
  
  Here's an example that demonstrates this concept by downloading data, writing it to a file, and then uploading the file. The `.catch()` block at the end handles any errors that may occur at any stage of the promise chain:
  
```javascript
function downloadData(url) {
  return new Promise(function executeDownload(resolve, reject) {
    console.log(`Downloading from ${url}`);

    setTimeout(() => {
      console.log("Download is complete");
      let downloadedData = "Some Data";
      resolve(downloadedData);
    }, 3000);
  });
}

function writeDataToFile(data, fileName) {
  return new Promise(function executeWrite(resolve, reject) {
    console.log(`Writing ${data} to file`);

    setTimeout(() => {
      console.log(`Writing to file ${fileName} is complete`);
      resolve(null);
    }, 2000);
  });
}

function uploadFile(fileName, url) {
  return new Promise(function executeUpload(resolve, reject) {
    console.log(`Uploading ${fileName} to ${url}`);

    setTimeout(() => {
      console.log("Upload is complete");
      let uploadStatus = "Success";
      resolve(uploadStatus);
    }, 1000);
  });
}

downloadData("https://example.com/data")
  .then(function handleDownload(downloadedData) {
    return writeDataToFile(downloadedData, "file.txt");
  })
  .then(function handleWrite() {
    return uploadFile("file.txt", "https://example.com/upload");
  })
  .then(function handleUpload(status) {
    console.log(status);
  })
  .catch(function (error) {
    console.log("Error:", error); // Handling any errors
  });
```

 **Explanation:**  
  In the above example, each `.then()` receives the result of the previous one and performs an operation on it, passing the new value to the next `.then()`, and the `.catch()` ensures that any failure in the chain is caught and handled. This structure is much more readable and manageable compared to nesting callbacks.

---
### **Promise API**

#### `Promise.all()`

- The **`Promise.all()`** static method takes an iterable of promises as input and returns a single `Promise`.
- This returned promise is fulfilled when **all** of the input promises are fulfilled. The fulfillment value is an array containing the results of all the promises in the order they were passed in.
- The time it takes for `Promise.all()` to fulfill depends on the promise that takes the longest to resolve.
- If any of the input promises reject, `Promise.all()` immediately rejects and returns the error for the first rejected promise.

**Example:**
```javascript
const p1 = new Promise((resolve, reject) => {
    setTimeout(() => {
        resolve('Promise 1 resolved'); // p1 resolves after 100ms
    }, 100);
});

const p2 = new Promise((resolve, reject) => {
    setTimeout(() => {
        reject('Promise 2 rejected'); // p2 rejects after 2000ms
    }, 2000);
});

const p3 = new Promise((resolve, reject) => {
    setTimeout(() => {
        resolve('Promise 3 resolved'); // p3 resolves after 300ms
    }, 300);
});

Promise.all([p1, p2, p3])
    .then(results => console.log(results))
    .catch(error => console.error(error));
```
**Explanation:** In this example, `Promise.all()` will reject immediately due to `p2` rejecting, and the output will be:  

```
Promise 2 rejected
```


#### `Promise.allSettled()`

- The **`Promise.allSettled()`** static method takes an iterable of promises as input and returns a single `Promise`.
- This returned promise fulfills when all of the input promises settle, providing an array of objects that describe the outcome of each promise.
- If any of the input promises reject, `Promise.allSettled()` does not immediately reject; it waits for all promises to settle, returning an array of the fulfillment values of fulfilled promises and the errors of rejected promises.

**Example:**
```javascript
Promise.allSettled([p1, p2, p3])
    .then(results => console.log(results))
    .catch(error => console.error(error));
```
**Explanation:** In this example, `Promise.allSettled()` will return an array showing that `p1` resolved, `p2` rejected, and `p3` resolved, and the output will look like: 

```
[
    { status: "fulfilled", value: "Promise 1 resolved" },
    { status: "rejected", reason: "Promise 2 rejected" },
    { status: "fulfilled", value: "Promise 3 resolved" }
]
```


#### `Promise.race()`

- The **`Promise.race()`** static method takes an iterable of promises as input and returns a single `Promise`.
- This returned promise settles with the eventual state of the first promise that settles. If fulfilled, it returns the value; if rejected, it returns the error.

**Example:**
```javascript
Promise.race([p1, p2, p3])
    .then(result => console.log(result))
    .catch(error => console.error(error));
```
**Explanation:** In this case, `Promise.race()` will log "Promise 1 resolved" because `p1` resolves before `p2` rejects. The output will be:  
```
Promise 1 resolved
```


#### `Promise.any()`

- The **`Promise.any()`** static method takes an iterable of promises as input and returns a single `Promise`.
- This returned promise fulfills when any of the input promises fulfill, providing the first fulfillment value.
- It rejects when all of the input's promises reject, returning an `AggregateError`, which is an array of all errors from the rejected promises. To handle this error, log `error.errors()`, which will show the array of errors.

**Example:**
```javascript
Promise.any([p1, p2, p3])
    .then(result => console.log(result))
    .catch(error => console.error(error));
```
**Explanation:** In this example, `Promise.any()` will fulfill with "Promise 1 resolved" since it is the first promise to fulfill, and the output will be:  
```
Promise 1 resolved
```

---
### Types of Programming Languages
Programming languages can be categorised into two main types:
1. **Imperative**: In imperative programming, you explicitly define *how* to accomplish a task, specifying the steps required to achieve the desired outcome.
2. **Declarative**: In declarative programming, you specify *what* you want to accomplish without detailing the exact steps on *how* it should be done.

---
### Iterators
- **Definition**: An iterator is a design pattern that enables writing declarative code. It is an object that allows you to traverse through a collection (such as an array or a string) one element at a time.
- **Example**:

  ```javascript
  const array = [1, 2, 3];
  const iterator = array[Symbol.iterator]();

  console.log(iterator.next()); // { value: 1, done: false }
  console.log(iterator.next()); // { value: 2, done: false }
  console.log(iterator.next()); // { value: 3, done: false }
  console.log(iterator.next()); // { value: undefined, done: true }
  ```

- **Custom Iterator Example**:
  You can implement a custom iterator using the following function:

  ```javascript
  function fetchNextElement(arr) {
    let idx = 0;

    function next() {
      if (idx >= arr.length) {
        return { value: undefined, done: true };
      }
      const newElement = arr[idx];
      idx++;
      return { value: newElement, done: false };
    }

    return { next };
  }

  const arr = [1, 2, 3, 4, 5];
  const autoFetcher = fetchNextElement(arr);

  console.log(autoFetcher.next()); // { value: 1, done: false }
  console.log(autoFetcher.next()); // { value: 2, done: false }
  console.log(autoFetcher.next()); // { value: 3, done: false }
  console.log(autoFetcher.next()); // { value: 4, done: false }
  console.log(autoFetcher.next()); // { value: 5, done: false }
  console.log(autoFetcher.next()); // { value: undefined, done: true }
  ```

---
### Generators
- **Definition**: A generator is a special type of function that can pause its execution and resume later. It is defined using the `function*` syntax and uses the `yield` keyword to return values.
- **Key Features**:
  - **`yield` Keyword**: Pauses the function's execution and returns a value. Execution resumes when `next()` is called again.
  - **`function*` Syntax**: Used to define a generator function.

- **Example**:
  ```javascript
  function* generatorFunction() {
    console.log("Line 1");
    yield 1;
    console.log("Line 2");
    yield 2;
    console.log("Line 3");
    yield 3;
  }

  const gen = generatorFunction();

  console.log(gen.next()); 
  console.log(gen.next()); 
  console.log(gen.next()); 
  console.log(gen.next()); 
  ```

- **Output:**
  ```
  Line 1
  { value: 1, done: false }
  Line 2
  { value: 2, done: false }
  Line 3
  { value: 3, done: false }
  { value: undefined, done: true }
  ```

- **Usage**:
  - **Lazy Evaluation**: Values are computed only when needed, making it useful for handling large datasets or infinite sequences.
  - **State Machines**: Generators can effectively manage complex state changes across multiple calls.

---
### Passing Values into Generators

Generators allow values to be passed back into the function using the `next()` method. 
- Here's an example:

```javascript
function* gen() {
  console.log("Inside Generator");
  const x = yield 10;
  const y = x + 30;
  yield y;
}

const it = gen();
console.log(it.next());       // Step 1
console.log(it.next(20));     // Step 2
```

**Explanation**:
1. **Step 1: `it.next()`**  
   - The generator starts executing, logging "Inside Generator" and yielding `10`.
   - The generator pauses, and the output is `{ value: 10, done: false }`.

2. **Step 2: `it.next(20)`**  
   - The generator resumes execution, receiving `20` as the value for `x`.
   - It calculates `y` as `x + 30`, resulting in `50`.
   - The generator then yields `50`, with the output `{ value: 50, done: false }`.

**Output**:
  ```
  Inside Generator
  { value: 10, done: false }
  { value: 50, done: false }
  ```

**Note**: If the `return` keyword is used in a generator function, any code after the `return` statement will not be executed.

---

### What is `async`? and What is `await`?

#### `async`: 
The keyword **`async`** is used to define an **`async function`**. When a function is declared as `async`, it automatically returns a **Promise**. If the function returns a value that is not a promise, JavaScript will wrap it in a resolved promise. This makes it easier to write asynchronous code, as it allows you to work with promises in a more readable way.

#### `await`:
The **`await`** keyword is used to pause the execution of an **`async`** function until a promise is resolved or rejected. It can only be used inside an **`async`** function. When used, it ensures that the next line of code does not run until the awaited promise settles.

#### Example:
```javascript
const p = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve('Data from API');
  }, 1000);
});

// Async and await
async function handlePromise() {
  const result = await p;
  console.log(result);
}

handlePromise();
// Output (after 1s):
// Data from API
```

---

### How `async` and `await` Work Behind the Scenes 


When using the `async` keyword, a function automatically returns a promise. Inside an `async` function, the `await` keyword allows JavaScript to handle asynchronous operations in a structured way. At the point where `await` is used, JavaScript returns from the function and continues executing other tasks in the event loop. Once the awaited promise resolves, the function resumes execution from that point with the resolved value.

Behind the scenes, `await` works like a generator’s `yield`. It pauses the function at that point, and when the promise resolves, it continues running the function with the promise’s result. This is similar to using `.then()` with promises, but `async/await` makes the code easier to read and write.

---

### Error Handling in `async/await`

In `async/await`, error handling is typically managed using a `try...catch` block. If a promise is rejected or an error occurs during the execution of an `async` function, the `catch` block catches and handles the error.

#### Example:
```javascript
const GITHUB_API = 'https://api.github.com/users/soumadip-dev';

async function fetchDataWithErrorHandling() {
  try {
    const data = await fetch(GITHUB_API);
    const response = await data.json();
    console.log(response);
  } catch (error) {
    console.error('Error:', error);
  }
}

fetchDataWithErrorHandling();
```

You can also handle errors by attaching `.catch()` directly to the async function call:

```javascript
fetchDataWithErrorHandling().catch(error => console.error('Error:', error));
```

#### Explanation:
- The `try` block contains the `await` calls to fetch the data. If an error occurs during the fetch operation (e.g., network issues or an invalid API endpoint), the `catch` block will execute, logging the error and preventing the script from breaking.
