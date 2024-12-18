# JavaScript

## Table of Contents

- [General](#general)
- [Object Notation](#object-notation)
- [Class](#class)
- [Encapsulation](#encapsulation)
- [Object](#object)
- [Map](#map)
- [Array](#array)
- [String](#string)
- [Promise](#promise)
- [Fetch/Async/Await](#fetchasyncawait)

## General

```javascript
setTimeout(fn, delay) // Execute fn after delay ms; return timerId

setInterval(fn, delay) // Execute fn at specified intervals; return intervalId

clearTimeout(timerId) // Cancels a timeout set by setTimeout().

clearInterval(intervalId) // Cancels a timer set by setInterval().

parseInt(string) // Converts a string to an integer.

parseFloat(string) // Converts a string to a floating-point number.

JSON.parse(jsonString, reviver(key, value, context)) // Converts jsonString into an object
// reviver() is run on parsed value before returning

JSON.stringify(value, replacer, space) // Converts an object to a JSON string
// replacer is function or array that replaces values; space is string or number to insert white space
```

## Object Notation

### Object Literal

Good for single instances or configuration objects

```javascript
const person = {
    name: 'Denzel',
    age: 50,
    greet: function() {
        return `Hello, my name is ${this.name} and I am ${this.age} years old.`;
    }
};

console.log(person.greet());  // Output: Hello, my name is Denzel and I am 50 years old.
```

### Prototype Pattern

Good for memory efficiency with large number of instances

```javascript
function Person(name, age) {
    this.name = name;
    this.age = age;
}

Person.prototype.greet = function() {
    return `Hello, my name is ${this.name} and I am ${this.age} years old.`;
};

const person = new Person('Denzel', 50);
console.log(person.greet());  // Output: Hello, my name is Denzel and I am 50 years old.
```

### Factory Function

Useful when creating instances with complex logic and states

```javascript
function Person(name, age) {
  return {
    name,
    age,
    greet() {
      return `Hello, my name is ${this.name} and I am ${this.age} years old.`;
    }
  }
}

const person = new Person('Denzel, 50);
console.log(person.greet()); // Output: Hello, my name is Denzel and I am 50 years old.
```

### Immediately Invoked Function Expressions

```javascript
const person = (function()  {
  const name = 'Denzel'
  const age = 50;

  return {
    name,
    age,
    gree() {
      return `Hello, my name is ${this.name} and I am ${this.age} years old.`;
    }
  };
})();

console.log(person.greet()); // Output: Hello, my name is Denzel and I am 50 years old.
```

## Class

Preferred way to define reusable object structures.

```javascript
class Person {
    constructor(name, age) {
        this.name = name;
        this.age = age;
    }

    greet() {
        return `Hello, my name is ${this.name} and I am ${this.age} years old.`;
    }
}

const person = new Person('Denzel', 50);
console.log(person.greet());  // Output: Hello, my name is Denzel and I am 50 years old.
```

### Encapsulation

Private and public methods and properties.

```javascript
class Person {
  // Public Properties
  name;
  age;

  // Private Properties
  #sin
  #address

  constructor(name, age, sin, address) {
    this.name = name;
    this.age = age;
    this.#sin = sin;
    this.#address = sin;
  }

  // Public Methods
  greet() {
    return `Hello, my name is ${this.name} and I am ${this.age} years old.`;
  }

  getMaskedSIN() {
    return `***-***-${this.#sin.slice(-3)}`;
  }

  updateAddress(newAddress) {
    this.#validateAddress(newAddress) && (this.#address = newAddress);
  }

  getAddress(sin) {
    if (this.#validateSIN(sin)) {
      return this.#address;
    } else {
      return null;
    }
  }

  // Private Methods
  #validateSIN(sin) {
    return sin === this.#sin;
  }

  #validateAddress(address) {
    return typeof address === 'string' && address.trim().length > 0;
  }
}

const person = new Person('Denzel', 50, '123456789', '123 place street');

console.log(person.getInfo()); // Output: Hello, my name is Denzel and I am 50 years old.

console.log(person.getMaskedSIN()); // Output: ***-***-789

person.updateAddress('456 place street');

console.log(person.getAddress('123456789')); // Output: 456 place street
```

## Object

Use an `Object` for:

- better performance on small datasets
- simple key-value pairs (strings/symbols)
- prototypal inheritance
- JSON support (`JSON.stringify` and `JSON.parse`)
- less complexity
- iteration: `for...in` or `Object.keys()`

### Static Methods

```javascript
const obj = {};

Object.keys(obj) // return array of strings of object's enumerable string-keyed property names

Object.getOwnPropertyNames() // return array of all of object's properties (except Symbols)

Object.values(obj) // returns array of object's enumerable string-keyed property values

Object.entries(obj) // returns array of object's enumerable string-keyed property key-value pairs

Object.assign(target, source1, source2, etc) // return copy of all enumerable own properties from one or more source objects to a target object

Object.hasOwn(obj, 'property') // return true if object has property

```

### Instance Methods

```javascript
const obj = {};

obj.hasOwnProperty('property') // prefer Object.hasOwn() for inheritance safety

obj.toString() // return string representing the object
```

## Map

Use a `map` for:

- insertion order preservation
- non-string keys
- frequent insertion/deletion
- map methods: `set()`, `get()`,  `delete()`, `has()`, `size`
- iteration: `forEach()` or `for...of`

### Static Methods

```javascript

```

### Instance Methods

```javascript
const map = new Map()

map.set(key, value) // adds/updates an entry with a specified key and value; return Map object

map.get(key) // return element associated with key

map.has(key) // return boolean if element in key exists

map.delete(key) // return boolean if element exists and is removed

map.clear() // remove all elements from map; return undefined
```

### Instance Properties

```javascript
map.size // return number of elements in map
```

## Array

Use an `Array` for:

- order matters
- numerical index-based access
- iteration over elements
- duplicates allowed
- array methods: `map()`, `filter()`, `reduce()`, `push()`, `pop()`
- iteration: `forEach()`, `for...of`, `for`, `map()` (for transformation)

### Static Methods

```javascript
Array.from('foo', fn, arg); // Output: `Array: ['f', 'o', 'o']`, fn to run on each, arg for `this` in fn

Array.fromAsync('foo'); // Same as Array.from() but also for async iterables

Array.isArray(arr); // boolean
```

### Instance Methods

```javascript
const arr = [];

arr.push(1, 2) // add to end of array; return length

arr.pop() // remove from end of array; return element

arr.shift() // remove from start of array; return element

arr.unshift(1, 2) // add to start of array; return length

arr.map(fn, arg) // call fn on each element in array; return new array

arr.filter(fn, arg) // fn returns truthy value run on each element in array
//fn arguments for current `element`, `index`, and `array`; return new array

arr.reduce(fn, initialValue) // fn run on each element in array, in order, passing the return value
// fn arguments for `accumulator` (value from previous call), `currentValue`, `currentIndex`, and `array`
// return single final result of running the reducer

arr.reduceRigt(fn, initialValue) // same as reduce() but right-to-left

arr.forEach(fn, arg) // call fn on each element in array; fn arguments: element, index, array; return undefined

arr.find(fn, arg) // return first element that satisfies test fn, else undefined
// fn arguments for `element`, `index`, `array`; arg is value for `this` in fn

arr.findIndex(fn, arg) // return the index of the first element that satisfies test fn, else undefined

arr.indexOf(searchElement, fromIndex) // return first index of searchElement, else -1

arr.includes(searchElement, fromIndex) // return true if searchElement found in array

arr.slice(start, end) // return shallow copy from index start up to end (does not include end)

arr.splice(start, deleteCount, item1, etc) // remove deleteCount elements from index start and insert item1, etc
// return array of removed elements

arr.join(separator) // return string with array elements separated by separator or comma
```

### Instance Properties

```javascript
arr.length // number of elements in array
```

## String

### Instance Methods

```javascript
const str = 'string';

str.charAt(index) // return string character at index

str.concat(str1, etc) // return string joined together

str.includes(searchString, fromIndex) // return true if str contains searchString (case-sensitive)

str.indexOf(searchString, fromIndex) // return index of the first occurrence of searchString

str.split(separator, limit) // return array of substrings split by separator up to limit substrings

str.substring(start, end) // return characters between start and end indeces

str.toLowerCase() // return string converted to lowercase

str.toUpperCase() // return string converted to uppercase

str.trim() // return string with whitespace removed from both sides

str.replace(pattern, replacement) // return string with pattern (string or regex) replaced by replacement
// replacement is string (replace first occurence only) or function (run on every match)

str.replaceAll(pattern, replacement) // return string with all mathces of pattern replaced by replacement
```

### Instance Properties

```javascript
String.length // number of characters in string, including spaces
```

## Promise

States: `pending`, `fulfilled`, `rejected`

```javascript
const promise1 = new Promise((resolve, reject) => {
	setTimeout(() => {
		resolve('foo');
	}, 300);
});
```

### Static Methods

```javascript
Promise.all(promises) // returns promise when all promises fulfilled, with an array of fulfillment values

Promise.race(promises) // returns promise with eventual state of first promise that settles

Promise.reject(reason) // shorthand for `new Promise((resolve, reject) => reject(reason))`

Promise.resolve(value) // shorthand for `new Promise((resolve) => resolve(value))`
```

### Instance Methods

```javascript
promise1
	.then(handleFulfilledA)
	.then(handleFulfilledB)
	.catch(handleError)
	.finally(handleEnd);
```

## Fetch/Async/Await

`async`: declares a function that returns a promise, allowing the use of `await` inside it

`await`: pauses execution until a promise resolves; return resolve result or throw reject error

```javascript
// Simulating an API request with delay using a Promise
// Function to fetch data from a given URL
function fetchData(url) {
  return fetch(url) // Return the promise from fetch
    .then(response => {
      if (!response.ok) {
        throw new Error("Network response was not ok"); // Handle HTTP errors
      }
      return response.json(); // Parse JSON if the response is okay
    });
}

// Async function using await and try...catch for error handling
async function getData(url) {
  try {
    const result = await fetchData(url); // Await fetchData promise
    console.log("Data fetched successfully:", result); // Logs the fetched data

    // Optional: you can await another promise or do something else after the first one
    const moreData = await fetchData(url); // Fetch data again for demonstration
    console.log("More data fetched successfully:", moreData); // Logs the fetched data

  } catch (error) {
    // Handles rejected promises (i.e., errors)
    console.error("Error fetching data:", error); // Logs error message
  }
}

// Example URL to fetch data from
const url = "https://jsonplaceholder.typicode.com/posts";

// Calling the async function
getData(url);
```
