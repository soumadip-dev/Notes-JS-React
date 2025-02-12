## What is an Array?

An `Array` is a special data structure used to store ordered collections.

---

## Declaration

There are two syntaxes for creating an empty array:

```javascript
let arr = new Array();
let arr = [];
```

Almost all the time, the second syntax is used. We can supply initial elements in the brackets:

```javascript
let items = ["Samosa", "Dosa", "Rasgulla"];
```

Array elements are numbered (or indexed), starting from zero.

We can get an element by its index using square brackets:

```javascript
let items = ["Samosa", "Dosa", "Rasgulla"];
alert(items[0]); // Samosa
alert(items[1]); // Dosa
alert(items[2]); // Rasgulla
```

---

## Modifying an Array

We can replace an element at a specific index:

```javascript
items[2] = "Mishti Doi"; // now ["Samosa", "Dosa", "Mishti Doi"]
```

…Or add a new one to the array:

```javascript
items[3] = "Pani Puri"; // now ["Samosa", "Dosa", "Mishti Doi", "Pani Puri"]
```

The total count of elements in the array is its `length`, and we can get the length of the array using the `.length` property.

```javascript
let items = ["Samosa", "Dosa", "Rasgulla"];
console.log(items.length); // 3
```

In JavaScript, an array can store elements of any type.  
For instance:

```javascript
// mix of values
let arr = [
  "Samosa",
  { name: "Raj" },
  true,
  function () {
    console.log("Namaste");
  },
]; // number, object, boolean, function here

// get the object at index 1 and then show its name
console.log(arr[1].name); // Raj

// get the function at index 3 and run it
arr[3](); // Namaste
```

---

## Get Last Elements with `.at()`

**Note:** This is a recent addition to the language. Older browsers may require polyfills. _(Polyfills are code snippets or libraries that provide modern functionality in browsers that do not support it natively.)_

Let’s say we want to retrieve the last element of an array.

Some programming languages allow negative indexing for this purpose, like `items[-1]`.

However, in JavaScript, this won’t work. The result will be `undefined` because an index inside square brackets is treated literally.

Traditionally, we calculate the last element’s index explicitly and then access it:

```js
let items = ['Samosa', 'Dosa', 'Rasgulla'];
console.log(items[items.length - 1]); // Rasgulla
```

This approach is slightly inconvenient since we have to write the variable name twice.

A shorter syntax is available: `items.at(-1)`:

```js
let items = ['Samosa', 'Dosa', 'Rasgulla'];
console.log(items.at(-1)); // Rasgulla
```

In other words, `arr.at(i)`:

- Works the same as `arr[i]` if `i >= 0`.
- For negative values of `i`, it accesses elements from the end of the array.

---

## Internals of Arrays

An array in JavaScript is a special type of object. The square bracket notation, `arr[0]`, is essentially the same as `obj[key]`, where `arr` is an object and numbers are used as keys.

Arrays extend objects by providing special methods for handling ordered collections of data, along with the `length` property. However, at their core, arrays are still objects and behave like them.

#### Arrays Are Copied by Reference
For instance: 

```JS
let items = ["Samosa"];
let arr = items; // Both variables reference the same array

arr.push("Dosa"); // Modify the array
console.log(items); // Output: [ "Samosa", "Dosa" ]
```

#### Optimizations and Misuse of Arrays

JavaScript engines optimize arrays by storing elements in a contiguous memory block. However, this optimization is lost if arrays are used like regular objects.

**Examples of improper usage:**

- Adding non-numeric properties: `arr.test = 5`
- Creating large gaps: `arr[0]` and `arr[1000]` (with nothing in between)
- Filling an array in reverse order

To maintain performance, always use arrays for ordered data. If you need arbitrary keys, use a regular object `{}` instead.

### Why Can't We Use `==` to Compare Arrays in JavaScript?

In JavaScript, **arrays are objects**, and the `==` operator does not compare objects by their contents. Instead, it checks whether they are the **same reference** in memory.

#### **Key Rules to Remember:**

1. **Two objects (including arrays) are only equal (`==`) if they are the same object in memory.**

```JS
let a = [];  
let b = [];  
console.log(a == b); // false  
```

2. **If one side of `==` is an object (like an array) and the other is a primitive (like a number or string), JavaScript converts the object to a primitive.**

```JS
console.log(0 == []);  // true  
console.log('0' == []); // false  
```

Here’s why:
- The empty array `[]` is converted to an **empty string** (`''`).
- Then JavaScript compares `0 == ''`, which is **true** (because `''` converts to `0`).
- But `'0' == ''` is **false** because they are two different strings.

#### **How to Properly Compare Arrays?**

Since `==` does not compare arrays element-by-element, the correct way to compare arrays is:

3. **Use a loop** to check each element manually.
4. **Use array methods like `.every()`** for comparison.

Example of correct array comparison:

```JS
function checkEqual(arr1, arr2) {
    if (arr1.length !== arr2.length) {
        return false;
    }
    return arr1.every((value, index) => value === arr2[index]);
}

console.log(checkEqual([1, 2, 3], [1, 2, 3])); // true  
console.log(checkEqual([1, 2, 3
```

---

## Array Methods: pop/push, shift/unshift

Arrays in JavaScript can work as both **queues** and **stacks**, allowing elements to be added or removed from either the beginning or the end.

### Queue (FIFO - First In, First Out)

A queue follows the FIFO principle, meaning the first added element is the first one to be removed.

- **push()** → Adds an element to the end.
- **shift()** → Removes an element from the beginning.

A common example is a queue of messages waiting to be displayed on a screen.

### Stack (LIFO - Last In, First Out)

A stack follows the LIFO principle, meaning the last added element is the first one to be removed.

- **push()** → Adds an element to the end.
- **pop()** → Removes an element from the end.

A stack can be visualized like a pile of books—new books are added and removed from the top.

### Methods for the End of an Array

#### pop() – Removes the last element and returns it

```javascript
let items = ["Samosa", "Dosa", "Rasgulla"];
console.log(items.pop()); // Removes "Rasgulla"
console.log(items); // ["Samosa", "Dosa"]
```

#### push() – Adds an element to the end

```javascript
let items = ["Samosa", "Dosa"];
items.push("Rasgulla");
console.log(items); // ["Samosa", "Dosa", "Rasgulla"]
```

### **Methods for the Beginning of an Array**

#### shift() – Removes the first element and returns it

```javascript
let items = ["Samosa", "Dosa", "Rasgulla"];
console.log(items.shift()); // Removes "Samosa"
console.log(items); // ["Dosa", "Rasgulla"]
```

#### unshift() – Adds an element to the beginning

```javascript
let items = ["Dosa", "Rasgulla"];
items.unshift("Samosa");
console.log(items); // ["Samosa", "Dosa", "Rasgulla"]
```

### Adding Multiple Elements at Once

Both `push()` and `unshift()` can add multiple elements:

```javascript
let items = ["Samosa"];
items.push("Dosa", "Sandesh");
items.unshift("Chai", "Kachori");

console.log(items); // ["Chai", "Kachori", "Samosa", "Dosa", "Sandesh"]
```

In computer science, an array that supports adding/removing elements from both ends is called a **deque (double-ended queue).**

### Performance 

The `push` and `pop` methods are fast, while `shift` and `unshift` are slow.

#### Why is working with the end of an array faster than the beginning?

Let’s break it down with an example:

```javascript
fruits.shift(); // Removes the first element
```

When `shift` is used, it's not just about removing the first element. The following operations take place:

5. The element at index `0` is removed.
6. All remaining elements are shifted left—index `1` becomes `0`, `2` becomes `1`, and so on.
7. The `length` property is updated.

The more elements an array has, the more time and memory this shifting process requires.

A similar issue occurs with `unshift`, which adds an element to the beginning. Before inserting, all existing elements must be moved to the right, increasing their indexes.

#### Why are `push` and `pop` faster?

With `push` and `pop`, no shifting is needed.

For example:

```javascript
fruits.pop(); // Removes the last element
```

Here’s what happens:

- `pop` simply removes the last element and updates `length`, without affecting the other indexes.
- `push` just adds a new element at the end without modifying existing indexes.

Since these operations don’t involve shifting, they are much faster.

---

## Array Method: `flat()`

The `Array.flat()` method in JavaScript is used to create a new array by flattening nested arrays up to a specified depth. It removes nesting and returns a single-level array based on the provided depth.

#### Syntax:

```JavaScript
array.flat(depth);
```

- **`depth`** _(optional)_: The number of levels to flatten.
    - Default value is `1`.
    - If set to `Infinity`, it flattens all levels completely.

#### Example:

```JavaScript
let arr = [1, [2, 3], [4, [5, 6]]];
let flatArr = arr.flat();
let flatArr2 = arr.flat(2);

console.log(flatArr);  // [1, 2, 3, 4, [5, 6]]
console.log(flatArr2); // [1, 2, 3, 4, 5, 6]
```

#### Flattening an Array Completely

If the depth is unknown, we can use `Infinity` to flatten the array entirely:

```JavaScript
let arr = [1, [2, 3], [4, [5, [6]]]];
let flatArr = arr.flat(Infinity);

console.log(flatArr); // [1, 2, 3, 4, 5, 6]
```

---

## Array Methods: splice, slice, and concat

### splice

Arrays are objects, so using `delete` on an array element leaves an empty slot, which isn't ideal:

```javascript
let items = ["Samosa", "Dosa", "Rasgulla"];
delete items[1];  
console.log(items); // ["Samosa", empty, "Rasgulla"]
console.log(items.length); // 3 (length remains unchanged)
```

Instead, use `splice`, which **removes, inserts, or replaces** elements properly:

**Syntax:**

```javascript
items.splice(start, optional delete count, elem1, elem2, ...);
```

- `start` → Index where modification begins.
- `deleteCount` → Number of elements to remove. (Set to `0` to insert only.)
- `elem1, elem2, ...` → Elements to insert at `start`.

#### Examples:

**Remove elements:**

```javascript
let items = ["Samosa", "Dosa", "Rasgulla"];
items.splice(1, 1); // Removes 1 element at index 1  
console.log(items); // ["Samosa", "Rasgulla"]
```

**Replace elements:**

```javascript
let items = ["Samosa", "Dosa", "Rasgulla", "Sandesh"];
items.splice(0, 2, "Chai", "Kachori");  
console.log(items); // ["Chai", "Kachori", "Rasgulla", "Sandesh"]
```

**Get removed elements:**

```javascript
let removed = items.splice(1, 2);  
console.log(removed); // ["Kachori", "Rasgulla"]
```

**Insert without deleting:**

```javascript
let items = ["Chai", "Sandesh"];
items.splice(1, 0, "Dhokla", "Pav Bhaji");  
console.log(items); // ["Chai", "Dhokla", "Pav Bhaji", "Sandesh"]
```

### slice

Unlike `splice`, `slice` does not modify the original array; instead, it **returns a shallow copy** of a portion of the array.

#### Syntax:

```javascript
items.slice(Optional start, Optional end);
```

- `start` → Index at which to begin extraction. (Optional, defaults to `0`)
- `end` → Index before which to stop extraction (not included). (Optional, defaults to the array length)

#### Examples

**Extract a portion**

The `slice` method extracts a section of an array without modifying the original array.

```javascript
let items = ["Samosa", "Dosa", "Rasgulla", "Kachori", "Sandesh"];
let sweets = items.slice(2, 4);  
console.log(sweets); // ["Rasgulla", "Kachori"]
```

**Copy the entire array**

We can create a shallow copy of an array by calling `slice()` without arguments.

```javascript
let items = ['Samosa', 'Dosa', 'Rasgulla', 'Kachori', 'Sandesh'];
let copy = items.slice();  
console.log(copy); // ["Samosa", "Dosa", "Rasgulla", "Kachori", "Sandesh"]
```

**Using negative indices**

We can use negative indices to extract elements from the end of the array.

```javascript
let items = ['Samosa', 'Dosa', 'Rasgulla', 'Kachori', 'Sandesh'];
console.log(items.slice(-4, -1)); // ['Dosa', 'Rasgulla', 'Kachori']
```

#### Modifying the copied array does not affect the original

Since `slice` creates a `shallow copy`, changes to the copied array do not modify the original array.

```javascript
let items = ['Samosa', 'Dosa', 'Rasgulla'];
let copy = items.slice();
copy[0] = 'Paratha';
console.log(items); // Still: ['Samosa', 'Dosa', 'Rasgulla']
```

### concat

The `concat` method is used to **merge two or more arrays**. It does not modify the original arrays but returns a **new array** containing elements from the provided arrays.

#### Syntax:

```javascript
let newArray = array1.concat(array2, array3, ...);
```

- `array1, array2, ...` → Arrays (or values) to merge into a new array.
- Returns a new array without modifying the originals.

#### Examples

**Merging two arrays:**

```javascript
let sweets = ["Rasgulla", "Kachori"];
let snacks = ["Samosa", "Dhokla"];
let food = sweets.concat(snacks);
console.log(food); // ["Rasgulla", "Kachori", "Samosa", "Dhokla"]
```

**Merging multiple arrays:**

```javascript
let sweets = ["Rasgulla", "Kachori"];
let snacks = ["Samosa", "Dhokla"];
let drinks = ["Chai", "Lassi"];
let combined = sweets.concat(snacks, drinks);
console.log(combined);
// ["Rasgulla", "Kachori", "Samosa", "Dhokla", "Chai", "Lassi"]
```

**Concatenating values:**

You can also pass individual values in addition to arrays.

```javascript
let sweets = ["Rasgulla", "Kachori"];
let foodWithExtras = sweets.concat("Pav Bhaji", ["Pani Puri", "Bhel Puri"]);
console.log(foodWithExtras);
// ["Rasgulla", "Kachori", "Pav Bhaji", "Pani Puri", "Bhel Puri"]
```

**Original arrays remain unchanged:**

Since `concat` returns a new array, the original arrays remain unmodified.

```javascript
console.log(sweets); // ["Rasgulla", "Kachori"]
console.log(snacks); // ["Samosa", "Dhokla"]
```

---

## Array Methods: `toString()`

The `toString()` method converts an array into a string of comma-separated values.

### Example:

```js
let items = ["Samosa", "Dosa", "Rasgulla"];
console.log(items.toString()); // "Samosa,Dosa,Rasgulla"
```

### Understanding Implicit Conversion with `+` Operator

Let’s examine how JavaScript converts arrays to strings when using the `+` operator:

```js
console.log([] + 1);       // "1"
console.log([1] + 1);      // "11"
console.log([1, 2] + 1);   // "1,21"
```

When the binary plus (`+`) operator is used with an array, JavaScript first converts the array to a string before concatenation.

- `[].toString()` → `""`, so `"" + 1` → `"1"`
- `[1].toString()` → `"1"`, so `"1" + 1` → `"11"`
- `[1, 2].toString()` → `"1,2"`, so `"1,2" + 1` → `"1,21"`

---

## Array Methods: `every()` and `some()`

### `.every()`

The `Array.every()` method in JavaScript is used to check whether **all** elements of an array satisfy a given condition. It returns `true` only if every element passes the test; otherwise, it returns `false`. If at least one element fails the condition, the result is `false`.

#### Syntax:

```JavaScript
array.every((element, index, array) => {/*...*/});
```

#### Example:

```JavaScript
let oddNumbers = [1, 3, 5, 7, 9];
let isOdd = oddNumbers.every(number => number % 2 !== 0);
console.log(isOdd); // true
```

### `.some()`

The `Array.some()` method in JavaScript is used to check whether **at least one** element in an array satisfies a given condition. It returns `true` if at least one element meets the condition; otherwise, it returns `false`.

#### Syntax:

```JavaScript
array.some((element, index, array) => {/*...*/});
```

#### Example:

```JavaScript
let numbers = [1, 2, 3, 4, 5];
let hasOdd = numbers.some(number => number % 2 !== 0);
console.log(hasOdd); // true
```

### Key Differences:

- **`every()`** checks if **all** elements pass the condition; if one fails, it returns `false`.
- **`some()`** checks if **at least one** element passes the condition; if none do, it returns `false`.

---

## Array Methods: Iteration with `forEach()`

The `forEach()` method allows executing a function on each element of an array.

### Syntax:

```js
arr.forEach(function(item, index, array) {
  // Perform an operation on item
});
```

#### Example

- Basic Iteration

```js
let items = ['Samosa', 'Dosa', 'Rasgulla'];

items.forEach(item => {
  console.log(item);
});
```

**Output:**

```
Samosa
Dosa
Rasgulla
```

- Accessing Index and Full Array

```js
let items = ['Samosa', 'Dosa', 'Rasgulla'];

items.forEach((item, index, array) => {
  console.log(
    `The item "${item}" is at index ${index} in the array [${array}].`
  );
});
```

**Output:**

```
The item "Samosa" is at index 0 in the array [Samosa,Dosa,Rasgulla].
The item "Dosa" is at index 1 in the array [Samosa,Dosa,Rasgulla].
The item "Rasgulla" is at index 2 in the array [Samosa,Dosa,Rasgulla].
```

---

## Array Methods: Searching with `indexOf()`, `lastIndexOf()`, and `includes()`

These methods are used to search for elements in an array.

### `indexOf()`

- The `indexOf()` method returns the **first index** of a specified element in an array. If the element is not found, it returns `-1`.
- `indexOf()` uses **strict equality (`===`)** for comparison. So, if we look for `false`, it finds exactly `false` and not `0`.

#### **Syntax:**

```js
arr.indexOf(element, fromIndex);
```

- `element`: The value to search for.
- `fromIndex` _(optional)_: The index to start the search from. Default is `0`.

#### **Example:**

```js
let arr = [1, 0, false, 'Samosa', 'Dosa', 'Rasgulla', 'Dosa'];
console.log(arr.indexOf(0));        // 1
console.log(arr.indexOf(false));    // 2
console.log(arr.indexOf(null));     // -1 (Not found)
console.log(arr.indexOf('Dosa', 5)); // 6 (Search starts from index 5)
```

### `lastIndexOf()`

- The `lastIndexOf()` method returns the **last index** of a specified element in an array. If the element is not found, it returns `-1`.
- It searches the array **backward**, starting from the specified `fromIndex`.

#### **Syntax:**

```js
arr.lastIndexOf(element, fromIndex);
```

- `element`: The value to search for.
- `fromIndex` _(optional)_: The index to start the search from (searching backward). Default is `arr.length - 1`.

#### **Example:**

```js
let items = ['Samosa', 'Dosa', 'Rasgulla', 'Dosa'];

console.log(items.lastIndexOf('Dosa'));    // 3
console.log(items.lastIndexOf('Kachori')); // -1 (Not found)
console.log(items.lastIndexOf('Dosa', 2)); // 1 (Search ends at index 2)
```

### `includes()`

- The `includes()` method checks whether an array contains a specified element. It returns `true` if found, otherwise `false`.
- Unlike `indexOf()`, it **does not return an index**—only a boolean value.

#### **Syntax:**

```js
arr.includes(element, fromIndex);
```

- `element`: The value to search for.
- `fromIndex` _(optional)_: The index to start the search from. Default is `0`.

#### **Example:**

```js
let items = ['Samosa', 'Dosa', 'Rasgulla'];

console.log(items.includes('Dosa'));    // true
console.log(items.includes('Kachori')); // false
console.log(items.includes('Dosa', 2)); // false (Search starts at index 2)
```

---

## Array Methods: Searching with a Condition using `find()`, `findIndex()`, `findLastIndex()`, and `filter`

These methods allow searching for elements based on a **condition**, rather than a strict match.

### `find()`

- The `find()` method returns the **first element** in an array that satisfies a given condition.
- If no element meets the condition, it returns `undefined`.

#### **Syntax:**

```js
arr.find(callback(element, index, array));
```

- `callback`: A function that defines the search condition.
- The function takes three parameters:
    - `element`: The current array element.
    - `index` _(optional)_: The index of the current element.
    - `array` _(optional)_: The array being searched.

#### **Example:**

```js
let numbers = [10, 20, 30, 40, 50];

let result = numbers.find(num => num > 25);
console.log(result); // 30 (first element greater than 25)
```

### `findIndex()`

- The `findIndex()` method returns the **index** of the first element that satisfies the given condition.
- If no element is found, it returns `-1`.

#### **Syntax:**

```js
arr.findIndex(callback(element, index, array));
```

#### **Example:**

```js
let numbers = [10, 20, 30, 40, 50];

let index = numbers.findIndex(num => num > 25);
console.log(index); // 2 (index of first element greater than 25)
```

### `findLastIndex()` (ES2023+)

- The `findLastIndex()` method is similar to `findIndex()`, but it searches **from the end of the array**.
- It returns the index of the **last** element that matches the condition or `-1` if not found.

#### **Syntax:**

```js
arr.findLastIndex(callback(element, index, array));
```

#### **Example:**

```js
let numbers = [10, 20, 30, 40, 50];

let index = numbers.findLastIndex(num => num > 25);
console.log(index); // 4 (last index of element greater than 25)
```

### `filter()`– Finding **All** Matches  ⭐⭐

- The `find()` method returns only the **first** matching element.
- If multiple elements satisfy the condition, use `filter()`, which returns **all matching elements** as an array.

#### **Syntax:**

```js
let results = arr.filter(callback(element, index, array));
```

- The syntax is similar to `find()`, but instead of returning a single element, `filter()` returns an **array** of all matching elements.
- If no elements match, it returns an **empty array**.

#### **Example:**

```js
let numbers = [10, 15, 20, 25, 30];

// Finding all odd numbers in the array
let oddNumbers = numbers.filter(num => num % 2 !== 0);
console.log(oddNumbers); // [15, 25]
```

---

## Array Methods: Transform using `map()` ⭐⭐

The `arr.map()` method is one of the most useful and frequently used array methods.

- It calls a function for **each element** of the array and returns a **new array** containing the results.
- The **original array remains unchanged**.

#### **Syntax:**

```js
let result = arr.map(function(item, index, array) {
    // Returns the new value instead of the item
});
```

#### **Example:**

Here, we double each number in the array:

```js
let numbers = [10, 15, 20, 25, 30];
const output = numbers.map(num => num * 2);

console.log(output); // [20, 30, 40, 50, 60]
console.log(numbers); // [10, 15, 20, 25, 30] (original array remains unchanged)
```

---

## Array Methods: `reduce()` ⭐⭐

The `reduce()` method is a powerful array method used to **process all elements** of an array and return a **single accumulated result**.

- It executes a **callback function** on each element of the array, passing the accumulated result from the previous iteration.
- It is often used for **sum, product, finding maximum/minimum values, and other cumulative computations**.

#### **Syntax:**

```js
let result = arr.reduce(function(accumulator, current, index, array) {
    // Process each element and return the updated accumulator
}, initialValue);
```

- `accumulator`: The running total or accumulated result.
- `current`: The current array element.
- `index` _(optional)_: The index of the current element.
- `array` _(optional)_: The array being processed.
- `initialValue`: The starting value of the accumulator (**optional but recommended**).

#### **Example:**

Let's first use a `for` loop and then achieve the same result using `reduce()`.

#### **Sum of Numbers**

```js
// Using for loop
const numbers = [5, 1, 3, 2, 6];
let sum = 0;
for (let i = 0; i < numbers.length; i++) {
    sum += numbers[i];
}
console.log(sum); // 17

//----------------

// Using reduce()
const numbers = [5, 1, 3, 2, 6];
const sum = numbers.reduce(function (acc, curr) {
    // acc = sum in for loop
    // curr = numbers[i]
    return acc + curr;
}, 0); // 0 is the initial value, similar to sum = 0 in the for loop
console.log(sum); // 17
```

#### **Finding the Maximum Value**

```js
// Using for loop
const numbers = [5, 1, 3, 2, 6];
let max = numbers[0];
for (let i = 1; i < numbers.length; i++) {
    if (numbers[i] > max) {
        max = numbers[i];
    }
}
console.log(max); // 6

//----------------

// Using reduce()
const numbers = [5, 1, 3, 2, 6];
const max = numbers.reduce(function (acc, curr) {
    return curr > acc ? curr : acc;
}, numbers[0]);
console.log(max); // 6
```

### **Key Points:**

1. `reduce()` **does not modify the original array**.
2. The **initial value** is crucial when dealing with **empty arrays** to prevent errors.
3. It can be used for **various operations**, including **sum, multiplication, flattening arrays, grouping elements, and more**.

---

## Polyfills for `map()`, `filter()`, and `reduce()`

### Polyfill for `map()`

```js
Array.prototype.myMap = function (cb) {
    let temp = [];
    for (let i = 0; i < this.length; i++) {
        temp.push(cb(this[i], i, this));
    }
    return temp;
};

const arr = [1, 2, 3, 4];
let output = arr.myMap(x => x * 2);
console.log(output); // [2, 4, 6, 8]
```

### Polyfill for `filter()`

```js
Array.prototype.myFilter = function (cb) {
    let temp = [];
    for (let i = 0; i < this.length; i++) {
        if (cb(this[i], i, this)) temp.push(this[i]);
    }
    return temp;
};

const arr = [1, 2, 3, 4];
let output = arr.myFilter(x => x % 2 === 0);
console.log(output); // [2, 4]
```

### Polyfill for `reduce()`

```js
Array.prototype.myReduce = function (cb, initialValue) {
    let accumulator = initialValue;
    for (let i = 0; i < this.length; i++) {
        accumulator = accumulator !== undefined ? cb(accumulator, this[i], i, this) : this[i];
    }
    return accumulator;
};

const arr = [1, 2, 3, 4];
let output = arr.myReduce((acc, curr) => acc + curr, 0);
console.log(output); // 10
```
---

## **Difference Between `map` and `forEach` in JavaScript**

#### **1. Return Value**

- `map` **returns a new array** with the modified values, whereas `forEach` **returns `undefined`**.
    
    ```javascript
    const arr = [2, 3, 5, 4, 7];
    
    const mapResult = arr.map(ar => {
      return ar * 2;
    });
    
    const forEachResult = arr.forEach(ar => {
      return ar * 2;
    });
    
    console.log(mapResult); // Output: [ 4, 6, 10, 8, 14 ] (New array)
    console.log(forEachResult); // Output: undefined
    ```
    

#### **2. Modification of Original Array**

- `map` does **not** modify the original array; instead, it creates a **new array**.
    
- `forEach`, on the other hand, **modifies the original array** when elements are reassigned.
    
    ```javascript
    arr.forEach((ar, i) => {
      arr[i] = ar + 3;
    });
    
    console.log(arr); // Output: [ 5, 6, 8, 7, 10 ] (Original array modified)
    ```
    

#### **3. Method Chaining**

- `map` **returns an array**, allowing **method chaining** (e.g., `.filter()`, `.reduce()`, etc.).
    
- `forEach` does **not return an array**, so method chaining is **not possible**.
    
    ```javascript
    const mapChaining = arr
      .map(ar => {
        return ar + 2;
      })
      .filter(x => x >= 6);
    
    console.log(mapChaining); // Output: New filtered array based on conditions
    ```

---
