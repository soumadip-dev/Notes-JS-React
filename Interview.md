### Variable Shadowing

In JavaScript, **variable shadowing** occurs when a variable declared within a certain scope (like a function or block) has the same name as a variable in an outer scope. When this happens, the inner scope "shadows" the outer one, meaning the inner variable takes precedence within its own scope, making the outer variable inaccessible in that scope.

Here’s an example to illustrate variable shadowing:

```javascript
let x = 10;

function exampleFunction() {
  let x = 20;  // This x shadows the outer x
  console.log(x);  // Output: 20
}

exampleFunction();
console.log(x);  // Output: 10
```

#### Illegal Shadowing

**Illegal shadowing** occurs when we try to shadow a `let` variable with a `var` variable within the same scope. This is not allowed in JavaScript and will result in an error.

```javascript
function test() {
  var a = "Hello";
  let b = "Bye";

  if (true) {
    let a = "Hi";   // Allowed: `let` shadowing `var`
    var b = "Goodbye";  // Error: 'b' has already been declared
    console.log(a);
    console.log(b);
  }
}
test();
```

In this example, attempting to shadow the `let` variable `b` with `var` within the same scope will cause an error.

--- 

### `var` vs `let` vs `const` declaration

- `var` can be redeclared and updated within the same scope.
- `let` can be updated but not redeclared in the same scope.
- `const` cannot be redeclared or updated.

Example:

```javascript
var x = 5;
var x = 10; // valid

let y = 5;
y = 10;     // valid
// let y = 20; // Error: cannot redeclare `y`

const z = 5;
// z = 10;    // Error: cannot reassign `z`
```


---
---

### What is `Object.seal()` in JavaScript?

`Object.seal()` is a method in JavaScript that seals an object. It prevents the addition or deletion of properties while still allowing modifications to the values of existing properties. This is useful when you want to keep the object's structure the same but still allow updates to its data.

```javascript
const product = { name: "iPhone 14 Pro", price: 125000 };
Object.seal(product);

product.company = "Apple"; // Not allowed, new properties cannot be added
console.log(product); // { name: "iPhone 14 Pro", price: 125000 }

delete product.price; // Not allowed, properties cannot be deleted
console.log(product); // { name: "iPhone 14 Pro", price: 125000 }

product.name = "iPhone 14 Pro Max"; // Existing properties can be modified
console.log(product); // { name: "iPhone 14 Pro Max", price: 125000 }
```

### What is `Object.freeze()` in JavaScript?

`Object.freeze()` is a method in JavaScript that freezes an object, making it immutable. This means that no properties can be added, deleted, or modified. The object's structure and data remain exactly as they were when the object was frozen. This is useful when you want to prevent any changes to an object.

```javascript
const product = { name: "iPhone 14 Pro", price: 125000 };
Object.freeze(product);

product.company = "Apple"; // Not allowed
console.log(product); // { name: "iPhone 14 Pro", price: 125000 }

delete product.price; // Not allowed
console.log(product); // { name: "iPhone 14 Pro", price: 125000 }

product.name = "iPhone 14 Pro Max"; // Not allowed
console.log(product); // { name: "iPhone 14 Pro", price: 125000 }
```

### What is `Object.preventExtensions()` in JavaScript?

`Object.preventExtensions()` is a method in JavaScript that prevents the addition of new properties to an object but allows the deletion and modification of existing properties' values.

```javascript
const product = { name: "iPhone 14 Pro", price: 125000 };
Object.preventExtensions(product);

product.company = "Apple"; // Not allowed
console.log(product); // { name: "iPhone 14 Pro", price: 125000 }

delete product.price; // Allowed
console.log(product); // { name: "iPhone 14 Pro" }

product.name = "iPhone 14 Pro Max"; // Allowed
console.log(product); // { name: "iPhone 14 Pro Max" }
```

### What are `Object.isFrozen()` and `Object.isSealed()`?

These methods check if an object is frozen or sealed.

```javascript
console.log(Object.isFrozen(product)); // true or false
console.log(Object.isSealed(product)); // true or false
```

---

### What are the different types of scope in JavaScript?

The types of scope in JavaScript are:
   - **Global Scope**
   - **Function Scope**
   - **Block Scope**

#### 1. Global Scope

Variables declared outside any function or block are in the global scope. These variables are accessible from anywhere in your code, whether inside a function, loop, or conditional statement.

**Example:**

```javascript
let x = 10;

function showX() {
    console.log(x); // Accessible here
}

showX(); // Outputs: 10

console.log(x); // Accessible here too
```

In the above code, `x` is declared in the global scope, so it can be accessed both inside and outside the `showX` function.

#### 2. Function Scope

When a variable is declared inside a function, it is scoped to that function, meaning it can only be accessed within that function.

**Example:**

```javascript
function showY() {
    let y = 20;
    console.log(y); // Accessible here
}

showY(); // Outputs: 20

console.log(y); // Error: y is not defined
```

Here, `y` is declared inside the `showY` function, so it is only accessible within that function and not outside.

#### 3. Block Scope

Block scope is created when variables are declared inside a pair of curly braces `{}`. This can happen within loops, conditionals, or just standalone blocks.

**Example:**

```javascript
if (true) {
    let z = 30;
    console.log(z); // Accessible here
}

console.log(z); // Error: z is not defined
```

In this example, `z` is declared inside an `if` block, so it is only accessible within that block.

### What is the difference between `let`, `var`, and `const`?

- `let` and `const` were introduced in ES6, while `var` is from older versions of JavaScript.
- Variables declared with `var` are function-scoped, meaning they are accessible throughout the entire function. `var` can also be globally scoped. `var` does not support block scope.
- `let` and `const` are block-scoped, meaning they are only accessible within the curly braces `{}`.
- Variables declared with `var` are attached to the `window` object, but `let` and `const` are not.

### What is function scope? How does it differ from block scope?

**Function scope** refers to variables being scoped to a function, meaning they are accessible throughout the function. **Block scope** refers to variables being scoped to a block `{}`, meaning they are only accessible within that block.

### What is lexical (or static) scope? Can you explain it with an example?

JavaScript uses **lexical scoping**, also known as static scoping. In lexical scoping, scopes are allocated during compile time. So, in JavaScript, values for variables are assigned in the execution phase, but the scope of the variable is decided during the compilation phase.

**Example:**

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

In the above code, `innerFunction` can access `outerVar` because it is lexically within the scope of `outerFunction`.

### What happens if you try to access a variable that is not in the current scope?

In JavaScript, when you try to access a variable, JavaScript looks for it in the following order:

1. **Current Scope**: It first checks the current function or block scope.
2. **Outer Scopes**: If not found, it looks in the outer functions or blocks.
3. **Global Scope**: Finally, it checks the global scope.

If the variable isn't found in any of these scopes, you'll get a `ReferenceError`.

```javascript
let globalVar = 'I am global'; // Global scope

function outerFunction() {
    let outerVar = 'I am outer'; // Outer function scope

    function innerFunction() {
        let innerVar = 'I am inner'; // Inner function scope
        console.log(innerVar);  // Outputs: 'I am inner'
        console.log(outerVar);  // Outputs: 'I am outer'
        console.log(globalVar); // Outputs: 'I am global'
        console.log(nonExistentVar); // Throws ReferenceError
    }

    innerFunction();
}

outerFunction();
```

---
### Difference Between `this` in Regular Functions and Arrow Functions

- **Regular Function:** In a regular function, `this` refers to the context in which the function was called, also known as the "call site." The call site can be an object, a position in the code, or it can be influenced by the `new` keyword.

- **Arrow Function:** In an arrow function, `this` is lexically bound, meaning it inherits `this` from the surrounding scope where the arrow function was defined.

```javascript
const obj = {
  x: 10,
  y: 20,
  outerFn: function () {
    const innerFn = () => {
      console.log(this.x, this.y);
    };
    innerFn();
  },
};

obj.outerFn(); 
```

In this code, `this` inside the arrow function `innerFn` is not determined by the function itself. Instead, it inherits `this` from its surrounding scope, which is the `outerFn` method. Since `outerFn` is a regular function and `this` within it refers to the `obj` object, `innerFn` also uses `this` from the `obj` object. As a result, `console.log(this.x, this.y);` outputs `10 20`.

---

### What is the purpose of the `static` keyword in JavaScript classes?

The `static` keyword in JavaScript classes is used to define methods or properties that belong to the class itself, rather than to instances of the class. Static methods and properties can be accessed directly from the class, without needing to instantiate it.

   ```javascript
   class Product {
     static getProductCategory() {
       return "Electronics";
     }

     static discountRate = 0.1;

     constructor(name, price) {
       this.name = name;
       this.price = price;
       console.log(`Accessing the static property: ${Product.discountRate}`);
     }
   }

   console.log(Product.getProductCategory()); // Output: "Electronics"
   const product1 = new Product("Laptop", 1500);
   ```
   
### What are `constructor functions`, and how do they work in JavaScript?
In JavaScript, constructor functions are a way to create objects with a common structure and behavior. Before the introduction of the `class` keyword in ES6, constructor functions were commonly used to create object blueprints. When using the `new` keyword with a constructor function:

1. A new object is created.
2. The `this` context of the function is set to the newly created object.
3. The function's properties and methods are attached to this new object.

```javascript
function Product(name, price, description) {
  this.name = name;
  this.price = price;
  this.description = description;
  this.displayProduct = function () {
    console.log(
      "Name:", this.name,
      "Price:", this.price,
      "Description:", this.description
    );
  };
}

let iphone = new Product("iPhone 11", 900, "Apple iPhone 11");
iphone.displayProduct();
// Output: Name: iPhone 11 Price: 900 Description: Apple iPhone 11
```

In this example, the `Product` constructor function is used to create a new `iphone` object with the specified properties and a method to display these properties.


2. **What is Object-Oriented Programming (OOP)? How does JavaScript support it?**
   - **Explanation:** Discuss the four main principles of OOP (Encapsulation, Inheritance, Polymorphism, and Abstraction) and how JavaScript implements them using objects, prototypes, and classes.

3. **Explain the concept of "prototypal inheritance" in JavaScript. How does it differ from classical inheritance?**
   - **Explanation:** Describe how JavaScript objects inherit properties from other objects via the prototype chain, as opposed to the class-based inheritance seen in languages like Java or C++.

4. **What is the difference between `__proto__` and `prototype` in JavaScript?**
   - **Explanation:** Clarify that `__proto__` is the actual object that is used in the lookup chain, while `prototype` is a property of a function object that is used when the function is used as a constructor with the `new` keyword.



5. **How do you implement inheritance in JavaScript? Can you show an example using both ES5 (function-based) and ES6 (class-based) syntax?**
   - **Explanation:** Provide an example of inheritance using constructor functions and the `Object.create` method for ES5, and classes and the `extends` keyword for ES6.

6. **What is the significance of the `super` keyword in ES6 classes?**
   - **Explanation:** Explain how `super` is used to call the constructor of a parent class or to access parent class methods in a derived class.

7. **What is method overriding in JavaScript? How is it achieved?**
   - **Explanation:** Describe how a subclass can provide a specific implementation of a method that is already defined in its parent class.

8. **Can you explain the concept of encapsulation with an example in JavaScript?**
   - **Explanation:** Discuss how encapsulation is implemented in JavaScript, often using closures or private fields (introduced in ES2022) to restrict direct access to an object's properties.

9. **What is the purpose of the `static` keyword in JavaScript classes?**
   - **Explanation:** Explain that `static` methods belong to the class itself rather than to instances of the class, and provide an example.

10. **How would you implement polymorphism in JavaScript?**
    - **Explanation:** Discuss method overloading (though not directly supported in JavaScript) and method overriding, and provide an example of how different classes can implement the same method in their own way.

These questions cover various aspects of OOP in JavaScript and help assess your understanding of how JavaScript handles object-oriented principles.

---

### Can you explain the difference between `==` and `===`?

- The `==` operator is called the **equality operator**, while the `===` operator is called the **strict equality operator**.
- Both operators check for equality, but `==` performs implicit type conversion, meaning it converts the operands to the same type before comparing them.
- In contrast, `===` does not perform any implicit type conversion and checks both the value and the type of the operands.

### Can you explain what higher-order functions are?

- **Higher-order functions** are functions that either accept another function as a parameter, return a function, or both.
- **Example:** The `forEach` method is a higher-order function because it takes another function as an argument.

---
# Async Await

### Given the following JavaScript code that utilizes Promises and `async`/`await`, what will be the order of the console log outputs, and why?

```javascript
const p1 = new Promise((resolve, reject) => {
    setTimeout(() => {
        resolve('Data from API 1');
    }, 10000);
});

const p2 = new Promise((resolve, reject) => {
    setTimeout(() => {
        resolve('Data from API 2');
    }, 500);
});

// Async and await
async function handlePromise() {
    console.log('Start processing');
  
    const result1 = await p1;
    console.log('Received from API 1');
    console.log(result1);
  
    const result2 = await p2;
    console.log('Received from API 2');
    console.log(result2);
}

handlePromise();
```

#### Follow-up Question:
- How would the behavior change if the `await` for `p1` and `p2` were swapped, and why?

#### Answer:

1. **Order of console log outputs:**
   - The first output will be `"Start processing"`, as it is logged synchronously before any `await`.
   - Since `p1` has a 10-second delay (setTimeout of 10,000 ms), the code will wait for the resolution of `p1`. After `p1` resolves, `"Received from API 1"` will be logged, followed by `"Data from API 1"`, the resolved value of `p1`.
   - Then, it will wait for the promise `p2`, which resolves much faster (500 ms). `"Received from API 2"` will be logged, followed by `"Data from API 2"`, the resolved value of `p2`.

 **Output sequence:**
```
Start processing
Received from API 1
Data from API 1
Received from API 2
Data from API 2
```

2. **If `await p2` comes before `await p1`:**
   - The code will first wait for `p2` (which resolves in 500 ms) before waiting for `p1` (which resolves in 10 seconds). Hence, `"Received from API 2"` and `"Data from API 2"` will be logged earlier, followed by `"Received from API 1"` and `"Data from API 1"`.

