# ES2015 Exercises

These exercises will just be done in markdown.

(For those unaware, there is a Table of Contents available to the left of the filename above.)

## let and const

### Refactor
ES5 Global Constants
```js
var PI = 3.14;
PI = 42; // Stop me from doing this!
```

ES2015 Global Constants
```js
const PI = 3.14;

// Also recommended when working with mutation:
const myArray = new Array; // Keeping a reference to an array.
```

### Quiz

1. What is the difference between `var` and `let`?
> Similar methods of variable declaration except that var has no block scope.
> `var` will not be block or loop local. Any usage in a loop or block will be global.
> Except for functions. `var` will stay within a function block.
> You can also redeclare with a `var` any number of times without error.
> They are also initialized at the start with `undefined`.
2. What is the difference between `var` and `const`?
> `const` variables cannot be reassigned or redeclared. `const` must also be initialized during declaration.
3. What is the difference between `let` and `const`?
> `const` variables cannot be reassigned.
4. What is hoisting?
> When the variables or functions are initialized before anything within their block.
> This allows you to invoke either variables or functions before they are declared.

## Arrow Functions

### Refactor
ES5 Map Callback
```js
function double(arr) {
    return arr.map(function(val) {
        return val * 2;
    });
}
```

ES2015 Arrow Functions Shorthand
```js
const double = arr => arr.map(val => val * 2);
```

### Refactor Again
Refactor the following function to use arrow functions:
```js
function squareAndFindEvens(numbers){
  var squares = numbers.map(function(num){
    return num ** 2;
  });
  var evens = squares.filter(function(square){
    return square % 2 === 0;
  });
  return evens;
}
```

```js
const squareAndFindEvens = numbers => numbers.map(num => num ** 2).filter(square => square % 2 === 0);
```

## Rest and Spread Operator

### Refactor
Given this function
```js
function filterOutOdds() {
  var nums = Array.prototype.slice.call(arguments);
  return nums.filter(function(num) {
    return num % 2 === 0
  });
}
```

Refactor it using the rest operator and arrow function
```js
const filterOutOdds = (...args) => args.filter(num => num % 2 === 0);
```

### findMin
Write a function called findMin that accepts a variable number of arguments and returns the smallest argument.

Make sure to do this using the rest and spread operator.
```js
findMin(1,4,12,-3) // -3
findMin(1,-1) // -1
findMin(3,1) // 1
```

The function:
```js
const findMin = (...args) => Math.min(...args);
```

### mergeObjects
Write a function called `mergeObjects` that accepts two objects and returns a new object which contains 
all the keys and values of the first object and second object.
```js
mergeObjects({a:1, b:2}, {c:3, d:4}) // {a:1, b:2, c:3, d:4}
```
The function:
```js
const mergeObjects = (object1, object2) => ({...object1, ...object2});
```

### doubleAndReturnArgs
Write a function called `doubleAndReturnArgs` which accepts an array and a variable number of arguments.
The function should return a new array with the original array values and all of the additional arguments doubled.
```js
doubleAndReturnArgs([1,2,3],4,4) // [1,2,3,8,8]
doubleAndReturnArgs([2],10,4) // [2, 20, 8]
```

The function:
```js
const doubleAndReturnArgs = (arr, ...args) => [...arr, ...args.map(num => num * 2)];
```

### Slice and Dice!
For this section, write the following functions using the rest and spread operators.
Refactor these functions to be arrow functions as well.

Make sure that you are always returning a new array or object, and not modifying existing inputs.
```js
/** remove a random element in the items array
and return a new array without that item. */

const removeRandom = items => {
    const itemIndex = Math.floor(Math.random() * items.length);
    return [...items.slice(0, itemIndex), ...items.slice(itemIndex + 1)];
}

/** Return a new array with every item in array1 and array2. */

const extend = (array1, array2) => [...array1, ...array2];

/** Return a new object with all the keys and values
from obj and a new key/value pair */

const addKeyVal = (obj, key, val) => ({...obj, [key]: val});

/** Return a new object with a key removed. */

const removeKey = (obj, key) => {
    ({ [key]: remove, ...obj} = obj);
    return obj;
}

/** Combine two objects and return a new object. */

const combine = (obj1, obj2) => ({...obj1, ...obj2});

/** Return a new object with a modified key and value. */

const update = (obj, key, val) => ({...obj, [key]: val});
```

## Object Enhancements

### Refactor

#### Same keys and values
```js
function createInstructor(firstName, lastName){
  return {
    firstName: firstName,
    lastName: lastName
  }
}
```

ES2015:
```js
function createInstructor(firstName, lastName){
  return {
    firstName,
    lastName
  }
}
```

#### Computed Property Names
```js
var favoriteNumber = 42;

var instructor = {
  firstName: "Colt"
}

instructor[favoriteNumber] = "That is my favorite!"
```

ES2015:
```js
let favoriteNumber = 42;

let instructor = {
    firstName: "Colt",
    [favoriteNumber]: "This is my favorite!"
}
```

#### Object Methods
```js
var instructor = {
  firstName: "Colt",
  sayHi: function(){
    return "Hi!";
  },
  sayBye: function(){
    return this.firstName + " says bye!";
  }
}
```

ES2015:
```js
let instructor = {
    firstName: "Colt",
    sayHi() { return "Hi!" },
    sayBye() { return this.firstName + " says bye!" },
}
```

### createAnimal function
Write a function which generates an animal object. The function should accept 3 arguments:
* _species: The species of animal ('cat', 'dog')._
* _verb: A string used to name a function ('bark', 'bleet')._
* _noise: A string to be printing when the above function is called ('woof', 'baaa')._
Use one or more of the object enhancements we've covered.
```js
const d = createAnimal("dog", "bark", "Woooof!")
// {species: "dog", bark: ƒ}
d.bark()  //"Woooof!"

const s = createAnimal("sheep", "bleet", "BAAAAaaaa")
// {species: "sheep", bleet: ƒ}
s.bleet() //"BAAAAaaaa"
```

The function:
```js
function createAnimal(species, verb, noise) {
    return {species, [verb]() { return noise } }
}
```