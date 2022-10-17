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

## Destructuring

### Object Destructuring 1
What does the following code return/print?
```js
let facts = {numPlanets: 8, yearNeptuneDiscovered: 1846};
let {numPlanets, yearNeptuneDiscovered} = facts;

console.log(numPlanets); // ?
console.log(yearNeptuneDiscovered); // ?
```
```js
console.log(numPlanets); // Prints out 8.
console.log(yearNeptuneDiscovered); // Prints out 1846.
```

### Object Destructuring 2
What does the following code return/print?
```js
let planetFacts = {
  numPlanets: 8,
  yearNeptuneDiscovered: 1846,
  yearMarsDiscovered: 1659
};

let {numPlanets, ...discoveryYears} = planetFacts;

console.log(discoveryYears); // ?
```

```js
console.log(discoveryYears); // Prints out the following object:

{
  yearMarsDiscovered: 1659,
  yearNeptuneDiscovered: 1846
}
```

### Object Destructuring 3
What does the following code return/print?
```js
function getUserData({firstName, favoriteColor="green"}){
  return `Your name is ${firstName} and you like ${favoriteColor}`;
}

getUserData({firstName: "Alejandro", favoriteColor: "purple"}) // ?
getUserData({firstName: "Melissa"}) // ?
getUserData({}) // ?
```

```js
getUserData({firstName: "Alejandro", favoriteColor: "purple"}) // returns:
"Your name is Alejandro and you like purple"

getUserData({firstName: "Melissa"}) // returns:
"Your name is Melissa and you like green"

getUserData({}) // returns:
"Your name is undefined and you like green"
```

### Array Destructuring 1
What does the following code return/print?
```js
let [first, second, third] = ["Maya", "Marisa", "Chi"];

console.log(first); // ?
console.log(second); // ?
console.log(third); // ?
```

```js
console.log(first); // Prints out "Maya".
console.log(second); // Prints out "Marisa".
console.log(third); // Prints out "Chi".
```

### Array Destructuring 2
What does the following code return/print?
```js
let [raindrops, whiskers, ...aFewOfMyFavoriteThings] = [
  "Raindrops on roses",
  "whiskers on kittens",
  "Bright copper kettles",
  "warm woolen mittens",
  "Brown paper packages tied up with strings"
]

console.log(raindrops); // ?
console.log(whiskers); // ?
console.log(aFewOfMyFavoriteThings); // ?
```

```js
console.log(raindrops); // Prints out "Raindrops on roses".
console.log(whiskers); // Prints out "whiskers on kittens".
console.log(aFewOfMyFavoriteThings); // Prints out the array:
["Bright copper kettles", "warm woolen mittens", "Brown paper packages tied up with strings"]
```

### Array Destructuring 3
What does the following code return/print?
```js
let numbers = [10, 20, 30];
[numbers[1], numbers[2]] = [numbers[2], numbers[1]]

console.log(numbers) // ?
```

```js
console.log(numbers) // Prints out [10, 30, 20].
```

### ES2015 Refactoring
In this exercise, you'll refactor some ES5 code into ES2015.

**ES5 Assigning Variables to Object Properties**
```js
var obj = {
  numbers: {
    a: 1,
    b: 2
  }
};

var a = obj.numbers.a;
var b = obj.numbers.b;
```

**ES2015 Object Destructuring**
```js
const obj = {
  numbers: {
    a: 1,
    b: 2
  }
};

const { a, b } = obj.numbers;
```

**ES5 Array Swap**
```js
var arr = [1, 2];
var temp = arr[0];
arr[0] = arr[1];
arr[1] = temp;
```

**ES2015 One-Line Array Swap with Destructuring**
```js
const arr = [1, 2];
[arr[0], arr[1]] = [arr[1], arr[0]]
```

### raceResults()
Write a function called raceResults which accepts a single array argument.
It should return an object with the keys **first, second, third** and **rest**.
* first: The first element in the array.
* second: The second element in the array.
* third: The third element in the array.
* rest: All other elements in the array.
  
**Write a one *line* function to make this work using**
* An arrow function
* Destructuring
* 'Enhanced' object assignment (same key/value shortcut)

```js
raceResults(['Tom', 'Margaret', 'Allison', 'David', 'Pierre'])
/*
  {
    first: "Tom",
    second: "Margaret",
    third: "Allison",
    rest: ["David", "Pierre"]
  }
*/
```

```js
const raceResults = ([first, second, third, ...rest]) => ({first, second, third, rest});
```

## Maps and Sets

### Quick Question 1
What does the following code return?
```js
new Set([1,1,2,2,3,4]);
```

A set object containing the values `1`, `2`, `3`, and `4`.

### Quick Question 2
What does the following code return?
```js
[...new Set("referee")].join("")
```

```js
"ref"
```

### Quick Question 3
What does the Map **m** look like after running the following code?
```js
let m = new Map();
m.set([1,2,3], true);
m.set([1,2,3], false);
```

```
[[1,2,3], true],
[[1,2,3], false]
```
### hasDuplicate
Write a function called hasDuplicate which accepts an array and returns true or false
if that array contains a duplicate.

```js
hasDuplicate([1,3,2,1) // true
hasDuplicate([1,5,-1,4]) // false
```
```js
const hasDuplicate = arr => new Set(arr).size !== arr.length;
```
### vowelCount
Write a function called vowelCount which accepts a string and returns a map
where the keys are numbers and the values are the count of the vowels in
the string.
```js
vowelCount('awesome') // Map { 'a' => 1, 'e' => 2, 'o' => 1 }
vowelCount('Colt') // Map { 'o' => 1 }
```

```js
function vowelCount(str){
    const vowels = 'aeiou';
    const vowelMap = new Map();
    str = str.toLowerCase();
    for (let char of str) {
        if (vowels.includes(char)) {
            if (vowelMap.has(char)) vowelMap.set(char, vowelMap.get(char) + 1);
            else vowelMap.set(char, 1);
        }
    }
    return vowelMap;
}
```

