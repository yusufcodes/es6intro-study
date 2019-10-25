# es6intro-study

This is a set of notes I've made from learning about ES6 from [The Complete JavaScript Course](https://www.udemy.com/course/the-complete-javascript-course/) in Section 7: Intro to ES6

## Variable Declarations with Let and Const

- const: Values that we want to be the same (constant)
- let: Values that we are able to mutate/change (similar to the old **var**)

Variables declared in the ES6 way are **block scoped**, as opposed to the old declaration of variables using var in ES5, which were **function scoped**.

Example: If you declare a variable within an if loop, these variables will only be accessible **within this if loop** only, and no where else within this function.

Block scoping refers to code wrapped within { ... }, so includes structures such as if, while, for, etc.

## Blocks and IIFEs

### Creation of a block

This isn't limited to structures such as if, else etc. - creating a block is possible by just writing: { ... }.

## Writing IIFEs

You can use the creation of a simple block: { ... } to create IIFE style methods. This saves you from having to write the following structure which was used in ES5:

```javascript
// ES5
(function() {
    // Code
})();

// ES6
{ 
    // Code
}
```

## Strings in ES6

- String Literals: Allows for you to add variables into a string, without the old concatenation method in ES5.

```javascript
// ES5
console.log('This is' + firstName + ' ' + lastName);

// ES6 - use backticks (`) instead of '
console.log(`This is ${firstName} ${lastName}`);

// Methods can also be placed with ${ ... }
```

- String Methods
  - startsWith('x'): Returns true if the string starts with x
  - endWith('x'): Returns true if the string ends with x
  - includes('x'): Returns true if the string contains the pattern specified ('x')
  - repeat(n): Repeats the string by the specified number of times (n)

## Arrow Functions

Functions can be written more simply with Arrow Functions. Below is a brief description of writing a basic function, followed by a comparison between ES5 and ES6.

- Function argument: el
- Function declaration: =>
- Function return: 2016 - el
  
```javascript
el => 2016 - el;
```

Below is a comparison of a function in ES5 and then a function in ES6.

### Example 1: Basic Function

```javascript
const years = [1990, 1965, 1982, 1937];

// ES5
var age5 = years.map(function(el) {
    return 2016 - el;
});

// ES6
const age6 = years.map(el => 2016 - el);
```

### Example 2: More Complex Function

Things to note in comparison to the first example:

- You must wrap function arguments in parentheses when there is more than 1
- You must wrap the function contents in curly braces when there is more than one line of code
- You must write the return keyword explicitly

```javascript
ages6 = years.map((el, index) => {
    const now = new Date().getFullYear();
    const age = now - el;
    return `Age element ${index + 1}: ${age}`;
});
```