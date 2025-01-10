## Important Object Methods

Consider the following object:

```javascript
let product = {
    name: "iPhone 14 Pro",
    company: "Apple",
    price: 125000,
    warranty: "1 Year",
    color: "Black",
};
```

### `Object.keys()`: Fetches All Unique Keys
This method returns an array of the object's property names (keys).

```javascript
Object.keys(product); 
// Output: ['name', 'company', 'price', 'warranty', 'color']
```

### `Object.values()`: Fetches All Values
This method returns an array of the values corresponding to the object's keys.

```javascript
Object.values(product); 
// Output: ['iPhone 14 Pro', 'Apple', 125000, '1 Year', 'Black']
```

### `Object.entries()`: Fetches Key-Value Pairs
This method returns an array of key-value pairs, where each pair is an array itself.

```javascript
Object.entries(product); 
// Output: [['name', 'iPhone 14 Pro'], ['company', 'Apple'], ['price', 125000], ['warranty', '1 Year'], ['color', 'Black']]
```

### Counting Key-Value Pairs

```javascript
Object.keys(product).length; 
// Output: 5
```

---
## Immutability in Objects

### `const` and Object Properties
Using `const` prevents reassignment of the variable, but the object's properties can still be modified, added, or deleted. When we create an object, the reference is stored in the variable, while the object itself is stored in heap memory. The `const` keyword only makes the reference to the object immutable, not the object itself.

```javascript
const obj = { x: 10, y: 20 };
obj.x = 99;          // Allowed: Updating a property
obj.z = 98;          // Allowed: Adding a new property
delete obj.z;        // Allowed: Deleting a property

// Reassigning a new object to the `const` variable will throw an error:
obj = { a: 10 };     // Error: Assignment to constant variable.
```

### Making Objects Immutable

#### `Object.seal()`
This method prevents adding or deleting properties but allows modification of existing ones.

```javascript
const product = { name: "iPhone 14 Pro", price: 125000 };
Object.seal(product);

product.company = "Apple"; // Not allowed: Adding new property
delete product.price; // Not allowed: Deleting property

product.name = "iPhone 14 Pro Max"; 
console.log(product); // Allowed: Modifying existing property
// Output: { name: "iPhone 14 Pro Max", price: 125000 }
```

#### `Object.freeze()`
This method prevents adding, deleting, or modifying properties.

```javascript
const product = { name: "iPhone 14 Pro", price: 125000 };
Object.freeze(product);

product.company = "Apple"; // Not allowed: Adding new property
delete product.price; // Not allowed: Deleting property
product.name = "iPhone 14 Pro Max"; // Not allowed: Modifying existing property
console.log(product); // Output: { name: "iPhone 14 Pro", price: 125000 }
```

#### `Object.preventExtensions()`
This method prevents adding new properties, but allows modification and deletion of existing properties.

```javascript
const product = { name: "iPhone 14 Pro", price: 125000 };
Object.preventExtensions(product);

product.company = "Apple"; // Not allowed: Adding new property
delete product.price; // Allowed: Deleting property
product.name = "iPhone 14 Pro Max"; 
console.log(product); // Allowed: Modifying existing property
// Output: { name: "iPhone 14 Pro Max" }
```

### `Object.isFrozen()` and `Object.isSealed()`
These methods check if an object is frozen or sealed, respectively.

```javascript
console.log(Object.isFrozen(product));  // true
console.log(Object.isSealed(product));  // true
```

### `Object.defineProperty()`
This method allows fine control over object properties, making them writable or configurable.

- **Writable**: Can the property value be updated?
- **Configurable**: Can the property be modified or deleted?

**Syntax**:

```javascript
Object.defineProperty(object, "key", {
    configurable: false,
    writable: false,
});
```

### Creating a Custom `Object.freeze()`
You can create your own version of `Object.freeze()` using `Object.preventExtensions()` and `Object.defineProperty()`.

```javascript
function customFreeze(obj) {
    let keys = Object.keys(obj);
    for (let i = 0; i < keys.length; i++) {
        Object.defineProperty(obj, keys[i], {
            configurable: false,
            writable: false,
        }); 
    }
    Object.preventExtensions(obj); // Prevents adding new properties
}
```


### `Object.assign()` in JavaScript

`Object.assign()` is a built-in JavaScript method used to copy properties from one or more source objects to a target object. It returns the target object after copying. The target object and the source object will reside at different locations in the heap memory, so changes made to the target object will not affect the source object. If the target object has properties with the same keys as those in the source object, the source properties will overwrite the target's.

- **target**: The object to which properties will be copied.
- **sources**: One or more source objects whose properties you want to copy to the target.

**Example:**
```javascript
const target = { a: 1 };
const source = { b: 2, c: 3 };
const source2 = { a: 3, c: 5 }; 
Object.assign(target, source, source2);
console.log(target); // Output: {a: 3, b: 2, c: 5}
```

#### Important Consideration:
`Object.assign()` performs a **shallow copy**, not a deep copy. This means that if the source object contains nested objects or arrays, those inner objects or arrays will still reference the same memory location as in the source object.

**Example:**
```javascript
const target = { a: 1 };
const source = { b: 2, c: 3, d: [5, 6] };
Object.assign(target, source);
target.d.push(7);
console.log(source.d); // Output: [5, 6, 7] --> The source object’s array is also modified
```

---
## Object Destructuring

`Object destructuring` is a convenient feature in JavaScript that allows you to extract properties from an object and assign them to variables. This simplifies the process of accessing object properties and reduces the need to use dot notation.

```javascript
const person = {
  name: 'Soumadip',
  age: 21,
  city: 'Durgapur'
};

const { name, age } = person;
console.log(name); // Soumadip
console.log(age);  // 21
```

In this example, the `name` and `age` properties of the `person` object are extracted directly into variables. By using curly braces with variable names that match the object properties, JavaScript unpacks the object and assigns the corresponding values to the variables. Note that the variable names must match the key names in the object; otherwise, the result will be `undefined`.

#### Default Values

You can assign **default values** to variables if the property does not exist in the object. If the property exists, its value will be used:

```javascript
const { name, country = 'USA' } = person;
console.log(country); // USA
```

#### Renaming Variables

Object destructuring allows you to `rename` extracted properties:

```javascript
const { name: fullName, age: personAge } = person;
console.log(fullName);  // Soumadip
console.log(personAge); // 21
```

#### Destructuring Nested Objects

To destructure nested objects, use additional curly braces:

```javascript
const product = {
  name: 'Iphone 14 Pro',
  price: 51000,
  category: { name: 'Mobiles', ID: 12 }
};

const { category: { name: categoryName } } = product;
console.log(categoryName); // Mobiles
```

#### Rest Parameter in Object

You can use the `rest` operator to collect the remaining properties of an object into a new object:

```javascript
const { name, ...otherDetails } = person;
console.log(name);          // Soumadip
console.log(otherDetails);  // { age: 21, city: 'Durgapur' }
```

In this example, the `rest` operator (`...otherDetails`) collects all remaining properties of the `person` object that were not explicitly destructured.

#### Spread Operator in Object

The `spread` operator can be used to create a new object by copying properties from an existing object:

```javascript
const newPerson = { ...person, country: 'India' };
console.log(newPerson);
// { name: 'Soumadip', age: 21, city: 'Durgapur', country: 'India' }
```

In this example, the `spread` operator (`...person`) copies all properties from the `person` object into `newPerson`. You can add or override properties as needed.

---
## Array Destructuring

All destructuring methods apply to arrays as well. The main difference is that, for arrays, we use square brackets `[]` instead of curly braces `{}`. 

When destructuring arrays, variable names don't matter; only their order does. This means you can assign any names to the variables, and they will receive values sequentially from the array.

```javascript
const [eng, bng, math, science] = [100, 200, 300, 400];
console.log(eng); // Prints 100
```

#### Using the Rest Operator in Array Destructuring

The rest operator `...` can be used to collect the remaining elements of an array into a new array.

```javascript
const [first, second, ...rest] = [10, 20, 30, 40, 50];
console.log(first);  // Prints 10
console.log(second); // Prints 20
console.log(rest);   // Prints [30, 40, 50]
```

The **rest parameter** syntax also allows a function to accept an indefinite number of arguments as an array:

```javascript
function sum(...theArgs) {
  let total = 0;
  for (const arg of theArgs) {
    total += arg;
  }
  return total;
}

console.log(sum(1, 2, 3)); // Output: 6
console.log(sum(1, 2, 3, 4)); // Output: 10
```

#### Using the Spread Operator with Arrays

The spread operator `...` expands an array into individual elements. This is helpful for combining arrays or passing array elements as arguments to functions.

```javascript
const numbers = [1, 2, 3];
const newNumbers = [...numbers, 4, 5];
console.log(newNumbers); // Prints [1, 2, 3, 4, 5]
```

In this example, `...numbers` spreads the elements of the `numbers` array into the `newNumbers` array.

---
## Autoboxing and Unboxing
In JavaScript, **autoboxing** and **unboxing** refer to the automatic conversion between primitive values (such as numbers, strings, and booleans) and their corresponding object types (such as `Number`, `String`, and `Boolean`).

#### 1. **Autoboxing**:
This is when JavaScript automatically converts a primitive value into its corresponding object wrapper class. This occurs when you try to access a method or property on a primitive value.

Example:

```js
let str = "Hello";
console.log(str.length); // Output: 5
```

In the above example, `"Hello"` is a primitive string. However, JavaScript automatically converts it into a `String` object (autoboxing) so that the `length` property can be accessed.

#### 2. **Unboxing**:
This is when JavaScript automatically converts an object wrapper back into its corresponding primitive value.

Example:

```js
let numObj = new Number(10); // Object wrapper
let result = numObj + 5;     // Unboxing happens here
console.log(result);         // Output: 15
```

Here, the `Number` object is automatically unboxed to the primitive number when performing arithmetic with it.
