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

## Arrow Functions: Lexical 'this' Keyword

Arrow functions **do not** have their own 'this' variable. Instead, they use the 'this' variable of the function they are written in.

It is for this reason that it is described to have a **lexical 'this' keyword.**

```javascript
function Person(name) {
    this.name = name;
}

Person.prototype.myFriends6 = friends => {
    let arr = frields.map(el => `${this.name} is friends with ${el}`);
};
```

## Destructuring

Destructuring is the process of breaking down a data structure into constituent variables. Examples below show how this is possible for **Arrays** and **Objects**.

### Arrays

```javascript
let foo = ['one', 'two', 'three'];

let [red, yellow, green] = foo;
console.log(red); // "one"
console.log(yellow); // "two"
console.log(green); // "three"
```

### Objects

```javascript
let o = {p: 42, q: true};
let {p, q} = o;

console.log(p); // 42
console.log(q); // true 
```

## Arrays in ES6

### Methods

- Array.from(x): Converts the input, x, into an Array.
- arrayName.findIndex(): Retrieve the index of the specificed value. A method can be passed into this.
- arrayName.find(): Retrieve the values which satisfies the condition passed into the method.

### Loops

The name of the new loop is called **for of**. It combines the features of a traditional for loop and the forEach loop, allowing for a more effective use of the for loop on an array. For example, you can now use the **continue** or **break** statement within this loop.

```javascript
// Change the value of the first and third elements only
arr = [1, 2, 3];
for (const cur of arr)
{
    if (cur.value === 2)
    {
        continue;
    }

    cur.value = 50;
}
```

## The Spread Operator

The operator looks like this: **...arrayName**, where each element is *expanded*. This means that each element is broken down into constituent parts, making it easy to list all the array elements. This also works on other structures, such as nodeLists.

```javascript
function addFourAges (a,b,c,d)
{
    return a+b+c+d;
}

var ages = [19, 32, 12, 18];

// The individual values of the ages array are passed into the method
const agesAdded = addFourAges(...ages);
```

## Function Parameters

### Rest Parameters

Allows for some arbituary arguments to be passed into a function, and from this, it will be transformed into an array, to be used within the function. It allows for standard parameters to be distinguished between arbituary ones.

```javascript
// ...years -> The years variable is available for us in this function, which will be 
// an array of all the arguments passed in.
function isFullAge(limit, ...years)
{
    years.forEach(cur => console.log((2016- cur) >= limit));
}
```

### Default Parameters

Allows for us to have pre-determined values for a parameter.

```javascript
// lastName has a default parameter of 'Smith'
function Person(firstName, yearOfBirth, lastName = 'Smith')
{
    // Code
};
```

## Maps - New Data Structure

A key:value data structure, allowing for any values to be used as keys. They can be better alternatives to using objects for the following reasons:

- Any value can be used as keys
- Can be iterated over using 'forEach' and 'for on'
- Size of the map is easily retrieved
- Data can easily be added/removed

```javascript
// Create a new Map
const question = new Map();

// Setting up key:value pairs with set()
question.set('question', 'What is the official name of the latest major version of JavaScript?')';
question.set(1, 'ES5');
question.set(2, 'ES6');
question.set(3, 'ES2015');
question.set(4, 'ES7');
question.set('correct', 3);
question.set(true, 'Correct!');
question.set(false, 'Incorrect');

// Retrieving values from the Map
question.get('question');

// Retrieve the size of the map
let size = question.size;

// Remove a value from the map
question.delete(4);

// Check if a key exists in the map
if (question.has(4))
{
    // Do something if true
}

// Delete ALL elements of the map
question.clear();

// forEach method on a map
question.forEach( (key, value) =>
console.log(`The ${key} with value ${value}`)
);

// for of method on a map
// entries() returns the key,value pairs, and then we use
// destructuring to store these values in key and value
for (let [key, value] of question.entries())
{
    // Code
};
```

## Classes

In ES5, Function Constructors are used for the definition of classes. We would then add methods to the prototype of the constructor to allow for them to be inherited.

```javascript
// ES5
var Person5 = function(name, yearOfBirth, job)
{
    this.name = name;
    this.yearOfBirth = yearOfBirth;
    this.job = job;
}

Person5.prototype.calculateAge = function()
{
    // Code
}

// ES6
// Defining the class
class Person6 {
    // All classes must have a constructor method
    constructor (name, yearOfBirth, job)
    {
        this.name = name;
        this.yearOfBirth = yearOfBirth;
        this.job = job;
    }

    calculateAge() 
    {
        // Code
    }

    // Static method - no instance of class needed to run these
    static greeting()
    {
        console.log('Hi!');
    }
}

// Creating an instance of the class
const john6 = new Person6('John', 1990, 'Teacher');

// Calling a static method
Person6.greeting();
```

## Classes with Subclasses

This section details how to go about inheriting from one class, the **super class** to another class, being the **sub class.** This is possible in both ES5 and ES6 with different implementations, so this is detailed below.

```javascript
// Creation of superclass, with a method added to its prototype
var Person5 = function(name, yearOfBirth, job) {
    this.name = name;
    this.yearOfBirth = yearOfBirth;
    this.job = job;
}

Person5.prototype.calculateAge = function() {
    var age = new Date().getFullYear() - this.yearOfBirth;
    console.log(age);
}

// Creation of subclass
var Athlete5 = function(name, yearOfBirth, job, olymicGames, medals) {
    // Setting the 'this' variable of Person5 to the Athlete5 object, allowing for us to inherit from this objects properties.
    Person5.call(this, name, yearOfBirth, job);

    // Adding our own properties, specific to an Athlete.
    this.olymicGames = olymicGames;
    this.medals = medals;
}

// Creating a new instance of Person5 and setting the prototype to the Athlete's prototype, giving us access to the Person5 methods.
Athlete5.prototype = Object.create(Person5.prototype);

// Adding our own method to the Athlete5 prototype. This will be inherited by any new Athlete5 instance.
Athlete5.prototype.wonMedal = function() {
    this.medals++;
    console.log(this.medals);
}

// Creating a new instance of an athlete and calling methods from the superclass and subclass
var johnAthlete5 = new Athlete5('John', 1990, 'swimmer', 3, 10);
johnAthlete5.calculateAge();
johnAthlete5.wonMedal();

// ES6

// Defining the superclass
class Person6
{
    // All classes must have a constructor method
    constructor (name, yearOfBirth, job)
    {
        this.name = name;
        this.yearOfBirth = yearOfBirth;
        this.job = job;
    }

    calculateAge() 
    {
        console.log('Age code here!');
    }
}

// Defining the subclass
class Athlete6 extends Person6
{
    constructor(name, yearOfBirth, job, olympicGames, medals)
    {
        // Super will make a call to the superclass constructor method
        super(name, yearOfBirth, job);
        this.olympicGames = olympicGames;
        this.medals = medals;
    }

    // Adding a method to the Athlete6 prototype property
    wonMedal() {
        this.medals++;
        console.log(this.medals);
    }
}

const johnAthlete6 = new Athlete6('John', 1990, 'swimmer', 3, 10);
johnAthlete6.wonMedal();
johnAthlete6.calculateAge();

```