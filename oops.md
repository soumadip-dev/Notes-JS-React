### What is OOP?
Object-Oriented Programming (OOP) is a paradigm that uses objects to model real-world entities. The core pillars of OOP are:

- **Encapsulation**: Bundles data and methods that operate on the data within a single unit (class).
- **Abstraction**: Simplifies complex systems by modeling classes appropriate to the problem.
- **Inheritance**: Allows a class to inherit properties and behavior from another class.
- **Polymorphism**: Enables objects to be treated as instances of their parent class, while specific actions are based on the actual class type.

---

### OOP in JavaScript
JavaScript supports OOP principles, allowing for the creation of classes, objects, and prototypes. There are three main ways to implement OOP in JavaScript:

  - **Constructor Functions and Prototypes**: A pre-ES6 method of creating objects and inheritance using functions and the `prototype` property.
  - **ES6 Classes**: Modern JavaScript syntax to define classes, which internally use constructor functions and prototypes.

#### Classes
Classes serve as blueprints for real-life entities, defining their structure and behavior. When we talk about how entities "look," we're referring to their properties. When we discuss how they "behave," we mean the actions or methods that can be performed on them.

**Note:** 
- Classes are first-class citizens because they are just wrappers of functions.
- Classes cannot be hoisted.

```javascript
class NameOfTheClass {
  // Details like member functions and data members go here
}
```

#### Objects
Objects are instances of classes and are created using the `new` keyword in JavaScript. This process is distinct from other languages.

```javascript
let iphone = new Product();
```

  - **`Object.create`**: Allows creating a new object with a specified prototype.

---

### Constructor
Every class in JavaScript includes a special method called a constructor. This method is automatically called when an object of the class is created. The constructor's default version is known as the default constructor, but you can provide your custom implementation.

```javascript
class Product {
  constructor() {
    // This is your custom constructor
  }
}
```

---

### How `new` Works
When you use `new`, it follows a four-step process:

1. Creates a new, empty object.
2. Calls the class's constructor, passing the new object as `this`. This allows the constructor to use `this` to refer to the new object.
3. Handles the necessary setup for prototypes (discussed later).
4. If the constructor explicitly returns an object, this object is assigned to the variable. If nothing or something other than an object is returned, the constructor ignores it.

---

### The `this` Keyword in JavaScript
In most cases, `this` refers to the context in which it was called, known as the "call site." The call site can be an object, a position in the code, or the `new` keyword. However, there is an exception when using arrow functions. In arrow functions, `this` is lexically bound, meaning it refers to the scope in which the arrow function was defined, not the call site.

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

**Note**: The `this` keyword does not point to the object where the method is created; it points to the object that is calling the method.

```javascript
const ram = {
  year: 1991,
  name: 'Ram',
  calcAge: function () {
    console.log(`Age of ${this.name} is ${2037 - this.year}`);
  },
};

const sam = {
  year: 1992,
  name: 'Sam',
};

ram.calcAge(); // Output: Age of Ram is 46 (this pointing to ram object)
sam.calcAge = ram.calcAge; // This is called object borrowing
sam.calcAge(); // Output: Age of Sam is 45 (this pointing to sam object)
```

In the above code, when `ram.calcAge()` is called, `this` refers to the `ram` object. But when `sam.calcAge()` is called after borrowing the method from `ram`, `this` refers to the `sam` object.

---

#### `call`, `apply`, and `bind` Methods

In JavaScript, `call`, `apply`, and `bind` are three very useful methods that allow you to control the value of the `this` keyword within a function.

- **`call`**: The `call` method allows you to explicitly set the value of `this` inside a function. It invokes the function with a specific `this` context and passes arguments individually.

```javascript
const myObj = {
    name: "Ram",
    greet: function(welcomeMessage, location) {
        console.log(`God ${this.name} ${welcomeMessage} to ${location}`);
    }
};

const newObj = {
    name: "Krishna"
};

myObj.greet.call(newObj, "Welcome", "Vrindavan"); 
// Output: God Krishna Welcome to Vrindavan
```

The `call` method allows us to pass the first argument as the new `this` context. If no object is passed, `this` refers to the global object. You can pass function parameters after the `this` reference.

- **`apply`**: The `apply` method is similar to `call`, but it takes two arguments:
    1. The object to which `this` will refer.
    2. An array of parameters to be passed to the function.

```javascript
// Using apply to set `this` to newObj and passing arguments as an array
myObj.greet.apply(newObj, ["Welcome", "Vrindavan"]);
// Output: God Krishna Welcome to Vrindavan
```

- **`bind`**: The `bind` method is similar to `call`, but it does not invoke the function immediately. Instead, it creates a new function with `this` permanently bound to the specified value, allowing you to call this new function later.

```javascript
// Create a new function with `this` bound to newObj 
const boundGreet = myObj.greet.bind(newObj);

// Another bound function with one pre-set argument
const boundGreet2 = myObj.greet.bind(newObj, "came");

// Call the bound functions
boundGreet("Welcome", "Vrindavan"); // Output: God Krishna welcomes you to Vrindavan
boundGreet2("Dwarka Nagri"); // Output: God Krishna came to Dwarka Nagri
```

We also use `bind` in situations where we want to call a method of an object that relies on `this`, especially from an event listener. If we call the method directly, `this` will refer to the element to which the event listener is attached.

```javascript
const button = document.querySelector("button"); // Suppose a button in HTML
const myObj = {
    name: "God Krishna",
    greet: function(location) {
        console.log(`${this.name} welcomes you to ${location}`);
    }
};

// button.addEventListener("click", myObj.greet); 
// This will throw an error because `this` points to the button element.

// Solution using bind
const boundGreetButton = myObj.greet.bind(myObj); // Bind the greet method to myObj
button.addEventListener('click', function() {
    boundGreetButton('Vrindavan');
}); // Output: God Krishna welcomes you to Vrindavan
```

**Note**: Arrow functions do not work with `call`, `apply`, and `bind` as they do not have their own `this`. The `this` context of arrow functions is lexically scoped based on where the arrow function is defined.

---

### What Is Prototype in JavaScript?

In JavaScript, when your code runs, the language sets up a built-in capital **`Object`** function in memory. Along with this function, an important unnamed object is created. This unnamed object isn't empty and contains essential JavaScript methods such as `toString()`, `isPrototypeOf()`, and `valueOf()`. We can access this unnamed object through **`Object.prototype`**.

```javascript
console.log(Object.prototype);

// Output:
// {}
// constructor: ƒ Object()
// isPrototypeOf: ƒ isPrototypeOf()
// propertyIsEnumerable: ƒ propertyIsEnumerable()
// toString: ƒ toString()
// valueOf: ƒ valueOf()
// __proto__: null
// toLocaleString: ƒ toLocaleString()
// [[Prototype]]: null
```

This object also contains a special **`constructor()`** function, which points back to the capital **`Object`** function.

```javascript
Object.prototype.constructor
// Output: ƒ Object() { [native code] }
```

When we define a function constructor or a class in JavaScript, an unnamed object is created automatically. This object can be accessed via `{class/functionName}.prototype`.

Methods defined within a function constructor are not stored in the prototype by default, as everything is inside the constructor. If we want to add a function to the prototype, we need to explicitly assign it to the prototype of that function using **`FunctionName.prototype.methodName = function() {}`**. In contrast, methods defined inside a class are stored in the prototype object automatically.

Additionally, this prototype includes a `constructor()` function that points back to the corresponding class or function.

```javascript
class Product {
  display() {
    console.log("Hello");
  }
}

console.log("1st Output:", Product.prototype);
console.log("2nd Output:", Product.prototype.constructor);

// Output:
// 1st Output: { display: ƒ }
// 2nd Output: class Product {
//   display() {
//     console.log("Hello");
//   }
// }
```

Finally, JavaScript links the class or function's prototype to **`Object.prototype`**.

![Prototype Image](/Images/prototype.png)


---

### Prototype Chain

JavaScript links the class or function's prototype to **`Object.prototype`**.

When we create an object from a class or function constructor using the `new` keyword, an empty object is created, and the class's constructor is called. This constructor modifies the new object, and a hidden link is established between the object and the prototype of the class.

Thus, the object is linked to the class's prototype, which in turn is linked to **`Object.prototype`**. This allows us to access methods from both prototypes. When you call a method from an object, JavaScript first checks if the method is defined on the object itself (via the constructor). If it isn't found, JavaScript looks for the method in the class's prototype, and if it's still not found, it searches in **`Object.prototype`**.

**This process of sharing methods between objects is known as prototyping.**

Here is an example demonstrating the prototype chain:
```javascript
// Define a class with a method
class ExampleClass {
  display() {
    return "Hello";
  }
}

// Create an instance of ExampleClass
let e1 = new ExampleClass();
console.log(e1.display()); // Access method from the ExampleClass prototype
console.log(e1.toString()); // Access method from Object.prototype

// Define a function with a prototype method
function ExampleFunction() {}
ExampleFunction.prototype.display = function() {
  return "Hello";
};

// Create an instance of ExampleFunction
let e2 = new ExampleFunction();
console.log(e2.display()); // Access method from the ExampleFunction prototype
console.log(e2.toString()); // Access method from Object.prototype
```

---

### `__proto__` Property

In JavaScript, every object has an internal property called **`[[Prototype]]`**, which can be accessed using the **`__proto__`** property. The **`__proto__`** property refers to the object's prototype, allowing it to inherit properties and methods from its prototype chain. This chain links the object to its class's prototype and eventually to **`Object.prototype`**.

```javascript
let p = new Product();
console.log(p.__proto__); // Outputs Product.prototype
console.log(p.__proto__.__proto__); // Outputs Object.prototype
```

In this example, `p.__proto__` points to `Product.prototype`, and `p.__proto__.__proto__` points to `Object.prototype`. This property is also called `dunder proto`.

---
### `Object.create()`

In JavaScript, the `Object.create()` method is used to create a new object with a specified prototype and optional properties. This is especially useful for setting up inheritance between objects.

#### Example:

```javascript
const personProto = {
  calcAge() {
    console.log(2024 - this.birthYear);
  },
  init(firstName, birthYear) {
    this.firstName = firstName;
    this.birthYear = birthYear;
  }
};

const rohit = Object.create(personProto);
rohit.init("Rohit", 1990);
rohit.calcAge(); // Output: 34
```

In this example, `rohit` inherits methods from `personProto`, allowing it to call `calcAge()` and other methods defined in the prototype object.

---

### `Static` Keyword in JavaScript
The `static` keyword in JavaScript is used to define methods or properties on a class that belong to the class itself, rather than instances of the class.

A common use case of the `static` keyword is in the builder design pattern, where it is used to implement a builder getter function.

Here’s an example of how the `static` keyword is used:

```javascript
class Product {
  // Static method
  static getProductCategory() {
    return "Electronics";
  }

  // Static property
  static discountRate = 0.1;

  constructor(name, price) {
    this.name = name;
    this.price = price;
    console.log(`Accessing the static property: ${Product.discountRate}`);
  }
}

// Accessing static method directly from the class
console.log(Product.getProductCategory()); // Output: "Electronics"

// Creating an instance of the Product class
const product1 = new Product("Laptop", 1500);
```


---

### Encapsulation and Data Security in JavaScript Classes

In JavaScript, classes do not inherently protect data members from being accessed or modified outside of the class, which can violate the principle of encapsulation in Object-Oriented Programming (OOP).

#### Protected Fields

While JavaScript doesn’t provide true `protected` fields, a common convention is to prefix a field with an underscore (`_`) to indicate that it should be treated as "protected." Although this convention doesn’t enforce actual protection, it serves as a visual reminder for developers to avoid accessing or modifying these fields outside the class or its subclasses.

```javascript
class Product {
  _name;
  _price;
  _description;

  displayProduct() {
    console.log(this._name, this._price, this._description); // Intended for internal use
  }
}

const item = new Product();
item._name = "Book"; // Still accessible outside the class, no true protection
```

#### Private Fields

To achieve genuine encapsulation and restrict access to within the class, JavaScript provides private fields. Private fields begin with a `#`, restricting access exclusively to the class itself, thereby ensuring true encapsulation.

```javascript
class Product {
  #name;
  #price;
  #description;

  displayProduct() {
    console.log(this.#name, this.#price, this.#description); // Accessible inside the class
  }
}

const item = new Product();
item.#name = "Book"; // Error: Private field '#name' must be declared in an enclosing class
```

By using private fields with the `#` prefix, JavaScript enforces data security and prevents accidental or unauthorized access from outside the class.

---

### `Getter` and `Setter` Methods
To manage access to these private members, getter and setter methods can be defined. These methods allow controlled read and write access, enabling validation and ensuring the integrity of the data.

```javascript
class Product {
  #price;

  getPrice() {
    return this.#price;
  }

  setPrice(p) {
    if (p > 0) {
      this.#price = p;
    } else {
      console.log("Invalid price");
    }
  }
}

let p = new Product();
p.setPrice(0); // Prints "Invalid price"
p.setPrice(500); // Sets the value of #price to 500
console.log(p.getPrice()); // Prints 500
```

Alternatively, the `get` and `set` keywords can be used to define getters and setters, making the syntax more concise and intuitive.

```javascript
class Product {
  #description;

  get description() {
    return this.#description;
  }

  set description(d) {
    if (d.length === 0) {
      console.log("Invalid description");
      return;
    }
    this.#description = d;
  }
}

const iphone = new Product();
iphone.description = "Something"; // Setter
console.log(iphone.description); // Getter --> Prints "Something"
```


---

### Prototype Inheritance with Constructor Functions

Prototype inheritance allows us to create a chain between parent and child classes by linking their prototypes. When using constructor functions, we can achieve this linkage in two ways:

1. **Using `__proto__` property**:
   ```javascript
   child.prototype.__proto__ = parent.prototype;
   ```
2. **Using `Object.create()`**:
   ```javascript
   child.prototype = Object.create(parent.prototype);
   ```

The main difference between these two methods is observed when accessing `child.prototype.constructor`. In the first method, it correctly refers to the child constructor function, while in the second method, it initially points to the parent constructor, and we need to manually set it back to the child.

In ES6 classes, the `super` keyword is used to call the parent class’s constructor. However, in constructor functions, we can achieve a similar result by using `call()` to explicitly invoke the parent constructor within the child constructor.

#### Example

Here’s an example demonstrating prototype inheritance between a parent `Event` constructor and a child `MovieEvent` constructor:

```javascript
// Parent constructor function: Event
function Event(name, date) {
  this.name = name;
  this.date = date;
}

// Adding a method to the parent prototype to describe the event
Event.prototype.getDetails = function () {
  return `Event: ${this.name} on ${this.date}`;
};

// Child constructor function: MovieEvent
function MovieEvent(movieName, date) {
  // Inherit properties from Event
  Event.call(this, movieName, date); // Set 'this' in Event to reference 'this' in MovieEvent
}

// Link the child's prototype to the parent's prototype
// Option 1: Using Object.create()
MovieEvent.prototype = Object.create(Event.prototype);

// Option 2: Using __proto__
// MovieEvent.prototype.__proto__ = Event.prototype;

// If using Object.create(), we need to reset the constructor property
MovieEvent.prototype.constructor = MovieEvent;

// Create an instance of MovieEvent
const movie = new MovieEvent("Inception", "25th September 2024");

console.log(movie.getDetails());
// Output: Event: Inception on 25th September 2024
```

In this example, `MovieEvent` inherits from `Event`, allowing instances of `MovieEvent` to access methods defined on `Event.prototype`, such as `getDetails()`.

![Inheritance Constructor Function](/Images/Inheritance_Constructor_function.png)


---

### Prototype Inheritance with ES6 Classes

In JavaScript, prototype inheritance is a method by which objects inherit properties and methods from other objects. Here are the key points:
Objects can inherit from other objects through a prototype chain. For example, a child object can inherit properties from a parent object via the prototype.
When a child class extends another parent class, the child class's prototype is connected to the prototype of the parent class. This allows the child class objects to access both the member functions of the parent class and the properties initialized in the parent class constructor using the `super()` keyword.

Here's an example demonstrating prototype inheritance in JavaScript:

```js
// Define the Event Class
class Event {
  // Constructor for the Event class
  constructor(type) {
    this.type = type; // Initialize the type of event
  }

  // Method to get event information **(present in Event.prototype)**
  getInfo() {
    return `This is an event of type: ${this.type}`; // Return a string describing the event type
  }
}

// Define the Movie Class inheriting from Event
class Movie extends Event {
  // Constructor for the Movie class
  constructor(type) {
    super(type); // Call the parent constructor to initialize type
  }
}

// Define the Comedy Class inheriting from Event
class Comedy extends Event {
  // Constructor for the Comedy class
  constructor(type) {
    super(type); // Call the parent constructor to initialize type
  }
}

// Create instances of Movie and Comedy
let m = new Movie("Movie"); // Create a Movie instance with type "Movie"
let c = new Comedy("Comedy"); // Create a Comedy instance with type "Comedy"

// Output the event information for Movie and Comedy instances
console.log(m.getInfo()); // The object of Movie class (m) can access getInfo because it extends the Event class
console.log(c.getInfo()); // The object of Comedy class (c) can access getInfo because it extends the Event class
```

In this example:
- Both `Movie` and `Comedy` classes inherit from the `Event` class.
- They both have access to the `getInfo` method defined in `Event`.
- The `super()` keyword is used to call the parent class's constructor and initialize the type property.

![[Inheritance_ES6_class.png]]
![Inheritance ES6 Class](/Images/Inheritance_ES6_class.png)

---

### Builder Design Pattern
Consider a class like this:

```javascript
class Product {
  #name;
  #price;
  #category;
  // ...
  constructor(name, description, price, category, discount) {
    this.name = name;
    this.price = price;
    this.description = description;
    // ...
  }
}
```

Here, the constructor has too many parameters, making it difficult to remember the order and value of each parameter. JavaScript does not support multiple constructors, so one approach is to use default values and getter/setter methods.

```javascript
class Product {
  #name;
  #price;
  #category;
  // ...
  get name() {
    /*...*/
  }
  set name(name) {
    /*...*/
  }
  get price() {
    /*...*/
  }
  set price(p) {
    /*...*/
  }
}
```

Using getters and setters can be limiting because we cannot validate the object before its creation. To address this, we can use a custom constructor and pass a single object (builder) that contains all the necessary properties.

```javascript
class Product {
  #name;
  #price;
  #category;
  // ...
  constructor(builder) {
    this.name = builder.name;
    if (builder.price > 0) this.price = builder.price;
    this.description = builder.description;
    // ...
  }
  get name() {
    /*...*/
  }
  set name(name) {
    /*...*/
  }
  get price() {
    /*...*/
  }
  set price(p) {
    /*...*/
  }
}
const p = new Product({
  name: "iPhone 11",
  price: 8700,
  description: "Apple iPhone",
});
```

This is a basic implementation of the Builder pattern. We can enhance it by introducing a static `Builder` class to create and configure product objects.

```javascript
class Product {
  #name;
  #price;
  #category;
  // ...
  constructor(builder) {
    this.name = builder.name;
    if (builder.price > 0) this.price = builder.price;
    this.description = builder.description;
    // ...
  }

  static get Builder() {
    class Builder {
      constructor() {
        this.name = ""; // Default values
        this.price = 0;
      }
      setName(name) {
        this.name = name;
        return this; // Allows method chaining
      }
      setPrice(price) {
        this.price = price;
        return this; // Allows method chaining
      }
      // Add more setters if needed
      build() {
        return new Product(this);
      }
    }
    return new Builder(); // Returns a new Builder instance
  }
  get name() {
    /*...*/
  }
  set name(name) {
    /*...*/
  }
  get price() {
    /*...*/
  }
  set price(p) {
    /*...*/
  }
}
```

### To use the Builder pattern with method chaining:

```javascript
const p = Product.Builder.setName("iPhone 11")
  .setPrice(1100)
  .setCategory("Smartphone")
  .build();
```


---

### How JavaScript OOP Differs from Languages like Java and C++

In languages like Java and C++, creating an object from a class means that any changes made to the class after the object is created do not affect the existing object. However, in JavaScript, modifying the prototype after object creation will reflect those changes in the already created object.

```JavaScript
function Product(a, b) {
    this.a = a;
    this.b = b;
}

Product.prototype.display = function() {
    console.log(this);
}

let p = new Product(2, 5);
p.display();  // Displays the current object properties

// Modify the prototype method
Product.prototype.display = function() {
    console.log("Modified", this);
}

p.display();  // Displays the modified output
```

In this example, after creating the object `p`, we modify the `display` function in `Product.prototype`. When `p.display()` is called again, it uses the modified method because JavaScript objects reference prototypes dynamically, allowing real-time changes.

This is why JavaScript is not considered a purely object-oriented language but rather **object-linked-to-other-object** language.
