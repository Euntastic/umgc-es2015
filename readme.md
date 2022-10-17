# ES2015 Exercises

These exercises will just be done in markdown.
(For those unaware, there is a Table of Contents available to the left of the filename above.)

## let and const

### ES5 Global Constants
```js
var PI = 3.14;
PI = 42; // Stop me from doing this!
```

### ES2015 Global Constants
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
   
    `const` variables cannot be reassigned or redeclared. `const` must also be initialized during declaration.
3. What is the difference between `let` and `const`?
   
    `const` variables cannot be reassigned.
4. What is hoisting?
   
    When the variables or functions are initialized before anything within their block.
    This allows you to invoke either variables or functions before they are declared.