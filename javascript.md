# JavaScript

## Array

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

## Object

### Static Methods

```javascript

```

### Instance Methods

```javascript

```

### Instance Properties

```javascript

```

## Map

### Static Methods

```javascript

```

### Instance Methods

```javascript

```

### Instance Properties

```javascript

```
