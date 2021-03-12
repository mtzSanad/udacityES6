# udacityES6 / ES2015
Trying out ES6 Features using course https://classroom.udacity.com/courses/ud356

# Syntax

## Let and Const

Variables declared with let and const eliminate this specific issue of hoisting because they’re scoped to the block, not to the function. Previously, when you used var, variables were either scoped globally or locally to an entire function scope.

If a variable is declared using let or const inside a block of code (denoted by curly braces { }), then the variable is stuck in what is known as the temporal dead zone until the variable’s declaration is processed. This behavior prevents variables from being accessed only until after they’ve been declared.

Variables declared with let can be reassigned, but can’t be redeclared in the same scope.

Variables declared with const must be assigned an initial value, but can’t be redeclared in the same scope, and can’t be reassigned.

### Use cases

* use let when you plan to reassign new values to a variable, and
* use const when you don’t plan on reassigning new values to a variable.

Since const is the strictest way to declare a variable, we suggest that you always declare variables with const because it'll make your code easier to reason about since you know the identifiers won't change throughout the lifetime of your program. If you find that you need to update a variable or change it, then go back and switch it from const to let.

What about var?
Is there any reason to use var anymore? Not really.

There are some arguments that can be made for using var in situations where you want to globally define variables, but this is often considered bad practice and should be avoided. From now on, we suggest ditching var in place of using let and const.

## Template literals

Prior to ES6, the old way to concatenate strings together was by using the string concatenation operator ( + )

```javascript
    const student = {
    name: 'Richard Kalehoff',
    guardian: 'Mr. Kalehoff'
    };

    const teacher = {
    name: 'Mrs. Wilson',
    room: 'N231'
    }

    let message = student.name + ' please see ' + teacher.name + ' in ' + teacher.room + ' to pick up your report card.';
```

This works alright, but it gets more complicated when you need to build multi-line strings.

```javascript
    let note = teacher.name + ',\n\n' +
    'Please excuse ' + student.name + '.\n' +
    'He is recovering from the flu.\n\n' +
    'Thank you,\n' +
    student.guardian;
```

** NOTE ** : As an alternative to using the string concatenation operator ( + ), you can use the String's concat() method, but both options are rather clunky for simulating true string interpolation.

Template literals are essentially string literals that include embedded expressions.

Denoted with backticks (` `) instead of single quotes ( '' ) or double quotes ( "" ), template literals can contain placeholders which are represented using ${expression}. This makes it much easier to build strings.

Here's the previous examples using template literals. Also note you can write the previous multi line example without \n

```javascript
    let message = `${student.name} please see ${teacher.name} in ${teacher.room} to pick up your report card.`;
```

## Destructing

In ES6, you can extract data from arrays and objects into distinct variables using destructuring.

Before ES6 you would do the following
```javascript
    const point = [10, 25, -34];

    const x = point[0];
    const y = point[1];
    const z = point[2];

    console.log(x, y, z);

    const gemstone = {
    type: 'quartz',
    color: 'rose',
    carat: 21.29
    };

    const type = gemstone.type;
    const color = gemstone.color;
    const carat = gemstone.carat;

    console.log(type, color, carat);
```

Destructuring borrows inspiration from languages like Perl and Python by allowing you to specify the elements you want to extract from an array or object on the left side of an assignment. It sounds a little weird, but you can actually achieve the same result as before, but with much less code; and it's still easy to understand.

With ES6 destructing

```javascript
    const point = [10, 25, -34];
    const [x,y,z] = point;
    console.log(x, y, z);

    const gemstone = {
    type: 'quartz',
    color: 'rose',
    carat: 21.29
    };
    const {type, color, carat} = gemstone;
    console.log(type, color, carat);
```

More examples https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment

## Object Literal Shorthand

Idea of removing repeatation.

You’ve probably written code where an object is being initialized using the same property names as the variable names being assigned to them.

```javascript
let type = 'quartz';
let color = 'rose';
let carat = 21.29;

const gemstone = {
  type: type,
  color: color,
  carat: carat
};

console.log(gemstone);
```

With ES6 you dont have to repeat your self

```javascript
let type = 'quartz';
let color = 'rose';
let carat = 21.29;

const gemstone = {
  type,
  color,
  carat
};

console.log(gemstone);
```

## Iteration

We have been using the traditional for loops for years using var i as following

```javascript
for(var i =0; i<= 5; i++){
    //do somthing
}
```

Now ES6 give us iterable interface and for...of loop

for...of loop combines the strengths of its siblings, the for loop and the for...in loop, to loop over any type of data that is iterable (meaning it follows the iterable protocol which we'll look at in lesson 3). By default, this includes the data types String, Array, Map, and Set—notably absent from this list is the Object data type (i.e. {}). Objects are not iterable, by default.

The for...in loop

The for...in loop improves upon the weaknesses of the for loop by eliminating the counting logic and exit condition.
But, you still have to deal with the issue of using an index to access the values of the array, and that stinks; it almost makes it more confusing than before.

```javascript
const digits = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9];

for (const index in digits) {
  console.log(digits[index]);
}
```

Also, the for...in loop can get you into big trouble when you need to add an extra method to an array (or another object). Because for...in loops loop over all enumerable properties, this means if you add any additional properties to the array's prototype, then those properties will also appear in the loop.

```javascript
Array.prototype.decimalfy = function() {
  for (let i = 0; i < this.length; i++) {
    this[i] = this[i].toFixed(2);
  }
};

const digits = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9];

for (const index in digits) {
  console.log(digits[index]);
}

Prints:
0
1
2
3
4
5
6
7
8
9
function() {
 for (let i = 0; i < this.length; i++) {
  this[i] = this[i].toFixed(2);
 }
}

//Gross! This is why for...in loops are discouraged when looping over arrays.
```

> NOTE: The forEach loop is another type of for loop in JavaScript. However, forEach() is actually an array method, so it can only be used exclusively with arrays. There is also no way to stop or break a forEach loop. If you need that type of behavior in your loop, you’ll have to use a basic for loop.

The for..of loop

```javascript
const digits = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9];

for (const digit of digits) {
  console.log(digit);
}
```

> TIP: It’s good practice to use plural names for objects that are collections of values. That way, when you loop over the collection, you can use the singular version of the name when referencing individual values in the collection. For example, for (const button of buttons) {...}.

But wait, there’s more! You can stop or break a for...of loop at anytime. And you don’t have to worry about adding new properties to objects. The for...of loop will only loop over the values in the object.

```javascript
const digits = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9];

for (const digit of digits) {
  if (digit % 2 === 0) {
    continue;
  }
  console.log(digit);
}
```

Finally getting both value and index, this syntax use array destructing

```javascript
for (const [i, v] of ['a', 'b', 'c'].entries()) {
  console.log(i, v)
}
```

## Spread Operator

The spread operator, written with three consecutive dots ( ... ), is new in ES6 and gives you the ability to expand, or spread, iterable objects into multiple elements.

```javascript
const primes = new Set([2, 3, 5, 7, 11, 13, 17, 19, 23, 29]);
console.log(...primes);

const books = ["Don Quixote", "The Hobbit", "Alice in Wonderland", "Tale of Two Cities"];
console.log(...books);
```

If you look at the output from the examples, notice that both the array and set have been expanded into their individual elements. So how is this useful?

Combining arrays with concat

```javascript
const fruits = ["apples", "bananas", "pears"];
const vegetables = ["corn", "potatoes", "carrots"];
const produce = fruits.concat(vegetables);
console.log(produce);
```

This could be better

```javascript
const fruits = ["apples", "bananas", "pears"];
const vegetables = ["corn", "potatoes", "carrots"];

const combine = [...fruits,...vegetables];

console.log(combine);
```

## Rest Operator

If you can use the spread operator to spread an array into multiple elements, then certainly there should be a way to bundle multiple elements back into an array, right?

The rest parameter, also written with three consecutive dots ( ... ), allows you to represent an indefinite number of elements as an array. This can be helpful in a couple of different situations.

```javascript
const order = [20.17, 18.67, 1.50, "cheese", "eggs", "milk", "bread"];
const [total, subtotal, tax, ...items] = order;
console.log(total, subtotal, tax, items);

function sum(...items){
    //do for item of items
}
```

Variadic functions
Another use case for the rest parameter is when you’re working with variadic functions. Variadic functions are functions that take an indefinite number of arguments.

```javascript
sum(1, 2);
sum(10, 36, 7, 84, 90, 110);
sum(-23, 3000, 575000);
```

This could be achieved using argument but it makes the function looks weierd as it will not have any argument in the definition

# Functions

## Arrow Function

ES6 introduces a new kind of function called the arrow function. Arrow functions are very similar to regular functions in behavior, but are quite different syntactically.

```javascript
//Regular function
const upperizedNames = ['Farrin', 'Kagure', 'Asser'].map(function(name) { 
  return name.toUpperCase();
});

//arrow function
const upperizedNames = ['Farrin', 'Kagure', 'Asser'].map(
  name => name.toUpperCase()
);
```

Steps to remove function to arrow

* remove the function keyword
* remove the parentheses
* remove the opening and closing curly braces
* remove the return keyword
* remove the semicolon
* add an arrow ( => ) between the parameter list and the function body

Regular functions can be either function declarations or function expressions, however arrow functions are always expressions. In fact, their full name is "arrow function expressions", so they can only be used where an expression is valid. This includes being:

* stored in a variable,
* passed as an argument to a function,
* and stored in an object's property.

```javascript
//arrow function stored in variable
const greet = name => `Hello ${name}!`;

// multiple parameters requires parentheses
const orderIceCream = (flavor, cone) => console.log(`Here's your ${flavor} ice cream in a ${cone} cone.`);
orderIceCream('chocolate', 'waffle');
```

** Concise and block body syntax **

Concise 

* has no curly braces surrounding the function body
* and automatically returns the expression

If you need more than just a single line of code in your arrow function's body, then you can use the "block body syntax".

```javascript
const upperizedNames = ['Farrin', 'Kagure', 'Asser'].map( name => {
  name = name.toUpperCase();
  return `${name} has ${name.length} characters in their name`;
});
```
If you need more than just a single line of code in your arrow function's body, then you can use the "block body syntax".

```javascript
const upperizedNames = ['Farrin', 'Kagure', 'Asser'].map( name => {
  name = name.toUpperCase();
  return `${name} has ${name.length} characters in their name`;
});
```

Important things to keep in mind with the block syntax:

* it uses curly braces to wrap the function body
* and a return statement needs to be used to actually return something from the function.

> WARNING: Everything's not all ponies and rainbows though, and there are definitely times when you might not want to use an arrow function. So before you wipe from your memory how to write a traditional function, check out these implications:rrow functions are only expressions there's no such thing as an arrow function declaration, there's a gotcha with the this keyword in arrow functions

## This in arrow function

"this" keyword value in normal function is dynamic depending on how a function is called

** In arrow function it depends on where the function is located in the code, "based on the function's surrounding context. I" **

Examples

1. A new object
If the function is called with new:

```javascript
const mySundae = new Sundae('Chocolate', ['Sprinkles', 'Hot Fudge']); 
```

In the code above, the value of this inside the Sundae constructor function is a new object because it was called with new.

2. A specified object
If the function is invoked with call/apply:

```javascript
const result = obj1.printName.call(obj2);
```

In the code above, the value of this inside printName() will refer to obj2 since the first parameter of call() is to explicitly set what this refers to.

3. A context object
If the function is a method of an object:

```javascript
data.teleport();
```

In the code above, the value of this inside teleport() will refer to data.

4. The global object or undefined
If the function is called with no context:

```javascript
teleport();
```

In the code above, the value of this inside teleport() is either the global object or, if in strict mode, it's undefined.

> Want more read book You don't know JS

Example

```javascript
// constructor
function IceCream() {
  this.scoops = 0;
}

// adds scoop to ice cream
IceCream.prototype.addScoop = function() {
  setTimeout(function() {
    this.scoops++;
    console.log('scoop added!');
  }, 500);
};

const dessert = new IceCream();
dessert.addScoop();

//Prints:
//scoop added!
```

After running the code above, you'd think that dessert.scoops would be 1 after half a millisecond. But, unfortunately, it's not:

```javascript
console.log(dessert.scoops);
//prints: 0
```

Can you tell why?

The function passed to setTimeout() is called without new, without call(), without apply(), and without a context object. That means the value of this inside the function is the global object and NOT the dessert object. So what actually happened was that a new scoops variable was created (with a default value of undefined) and was then incremented (undefined + 1 results in NaN):

One way around this is to use closure:

```javascript
// constructor
function IceCream() {
  this.scoops = 0;
}

// adds scoop to ice cream
IceCream.prototype.addScoop = function() {
  const cone = this; // sets `this` to the `cone` variable
  setTimeout(function() {
    cone.scoops++; // references the `cone` variable
    console.log('scoop added!');
  }, 0.5);
};

const dessert = new IceCream();
dessert.addScoop();
```

Well that's exactly what arrow functions do, so let's replace the function passed to setTimeout() with an arrow function:

```javascript
// constructor
function IceCream() {
  this.scoops = 0;
}

// adds scoop to ice cream
IceCream.prototype.addScoop = function() {
  setTimeout(() => { // an arrow function is passed to setTimeout
    this.scoops++;
    console.log('scoop added!');
  }, 0.5);
};

const dessert = new IceCream();
dessert.addScoop();
```

Since arrow functions inherit their this value from the surrounding context, this code works!

When addScoop() is called, the value of this inside addScoop() refers to dessert. Since an arrow function is passed to setTimeout(), it's using its surrounding context to determine what this refers to inside itself. So since this outside of the arrow function refers to dessert, the value of this inside the arrow function will also refer to dessert.

Now what do you think would happen if we changed the addScoop() method to an arrow function?

```javascript
// constructor
function IceCream() {
    this.scoops = 0;
}

// adds scoop to ice cream
IceCream.prototype.addScoop = () => { // addScoop is now an arrow function
  setTimeout(() => {
    this.scoops++;
    console.log('scoop added!');
  }, 0.5);
};

const dessert = new IceCream();
dessert.addScoop();
```

Yeah, this doesn't work for the same reason - arrow functions inherit their this value from their surrounding context. Outside of the addScoop() method, the value of this is the global object. So if addScoop() is an arrow function, the value of this inside addScoop() is the global object. Which then makes the value of this in the function passed to setTimeout() also set to the global object!

## Default function parameters

Ugly without ES6

```javascript
function greet(name, greeting) {
  name = (typeof name !== 'undefined') ?  name : 'Student';
  greeting = (typeof greeting !== 'undefined') ?  greeting : 'Welcome';

  return `${greeting} ${name}!`;
}

greet(); // Welcome Student!
greet('James'); // Welcome James!
greet('Richard', 'Howdy'); // Howdy Richard!
```

with ES6

```javascript
function greet(name = 'Student', greeting = 'Welcome') {
  return `${greeting} ${name}!`;
}

greet(); // Welcome Student!
greet('James'); // Welcome James!
greet('Richard', 'Howdy'); // Howdy Richard!
```

## Defaults and destructring arrays / objects

You can combine default function parameters with destructuring to create some pretty powerful functions!

```javascript
 function createGrid([width = 5, height = 5]) {
  return `Generates a ${width} x ${height} grid`;
}

createGrid([]); // Generates a 5 x 5 grid
createGrid([2]); // Generates a 2 x 5 grid
createGrid([2, 3]); // Generates a 2 x 3 grid
createGrid([undefined, 3]); // Generates a 5 x 3 grid
```

if called createGrid() this will give error because it expects an array even if it was empty, so solution is to default it too

```javascript
 function createGrid([width = 5, height = 5] = []) {
  return `Generates a ${width} x ${height} grid`;
}
```

For Objects

```javascript
 function createSundae({scoops = 1, toppings = ['Hot Fudge']}) {
  const scoopText = scoops === 1 ? 'scoop' : 'scoops';
  return `Your sundae has ${scoops} ${scoopText} with ${toppings.join(' and ')} toppings.`;
}

createSundae({}); // Your sundae has 1 scoop with Hot Fudge toppings.
createSundae({scoops: 2}); // Your sundae has 2 scoops with Hot Fudge toppings.
createSundae({scoops: 2, toppings: ['Sprinkles']}); // Your sundae has 2 scoops with Sprinkles toppings.
createSundae({toppings: ['Cookie Dough']}); // Your sundae has 1 scoop with Cookie Dough toppings.
```

Defaulting  object it self

```javascript
 function createSundae({scoops = 1, toppings = ['Hot Fudge']} = {}) {
  const scoopText = scoops === 1 ? 'scoop' : 'scoops';
  return `Your sundae has ${scoops} ${scoopText} with ${toppings.join(' and ')} toppings.`;
}
```

Array defaults vs. object defaults
Default function parameters are a simple addition, but it makes our lives so much easier! One benefit of object defaults over array defaults is how they handle skipped options. Check this out:

```javascript
function createSundae({scoops = 1, toppings = ['Hot Fudge']} = {}) { … } 
```

...with the createSundae() function using object defaults with destructuring, if you want to use the default value for scoops but change the toppings, then all you need to do is pass in an object with toppings:

```javascript
 createSundae({toppings: ['Hot Fudge', 'Sprinkles', 'Caramel']});
```
Compare the above example with the same function that uses array defaults with destructuring.

```javascript
function createSundae([scoops = 1, toppings = ['Hot Fudge']] = []) { … } 
```
With this function setup, if you want to use the default number of scoops but change the toppings, you'd have to call your function a little...oddly:

createSundae([undefined, ['Hot Fudge', 'Sprinkles', 'Caramel']]);
Since arrays are positionally based, we have to pass undefined to "skip" over the first argument (and accept the default) to get to the second argument.

Unless you've got a strong reason to use array defaults with array destructuring, we recommend going with object defaults with object destructuring!

## Class

Preview

```javascript
 class Dessert {
  constructor(calories = 250) {
    this.calories = calories;
  }
}

class IceCream extends Dessert {
  constructor(flavor, calories, toppings = []) {
    super(calories);
    this.flavor = flavor;
    this.toppings = toppings;
  }
  addTopping(topping) {
    this.toppings.push(topping);
  }
}
```

JS is not class base ES6 syntax use under hood function and prototype to get the effect of class

ES5 work that is done automaticlly in ES6 using the above keywords

```javascript
 function Plane(numEngines) {
  this.numEngines = numEngines;
  this.enginesActive = false;
}

// methods "inherited" by all instances
Plane.prototype.startEngines = function () {
  console.log('starting engines...');
  this.enginesActive = true;
};

var richardsPlane = new Plane(1);
richardsPlane.startEngines();

var jamesPlane = new Plane(4);
jamesPlane.startEngines();
```

using ES6

```javascript
 class Plane {
  constructor(numEngines) {
    this.numEngines = numEngines;
    this.enginesActive = false;
  }

  startEngines() {
    console.log('starting engines…');
    this.enginesActive = true;
  }
}
```

Class is function
```javascript
 class Plane {
  constructor(numEngines) {
    this.numEngines = numEngines;
    this.enginesActive = false;
  }

  startEngines() {
    console.log('starting engines…');
    this.enginesActive = true;
  }
}

typeof Plane; // function
```

> Did you notice that there aren't any commas between the method definitions in the Class? Commas are not used to separate properties or methods in a Class. If you add them, you'll get a SyntaxError of unexpected token ,

## Static methods

```javascript
 class Plane {
  constructor(numEngines) {
    this.numEngines = numEngines;
    this.enginesActive = false;
  }

  static badWeather(planes) {
    for (plane of planes) {
      plane.enginesActive = false;
    }
  }

  startEngines() {
    console.log('starting engines…');
    this.enginesActive = true;
  }
}

Plane.badWeather([plane1, plane2, plane3]);
```

> IN Depth course regarding Object Oriented in JS https://classroom.udacity.com/courses/ud711

Benefits of classes
* Less setup
* There's a lot less code that you need to write to create a function
* Clearly defined constructor function
* Inside the class definition, you can clearly specify the constructor function.
* Everything's contained
* All code that's needed for the class is contained in the class declaration. Instead of having the constructor function in one place, then adding methods to the prototype one-by-one, you can do everything all at once!

Things to look out for when using classes
* class is not magic
* The class keyword brings with it a lot of mental constructs from other, class-based languages. It doesn't magically add this functionality to JavaScript classes.
class is a mirage over prototypal inheritance
* We've said this many times before, but under the hood, a JavaScript class just uses prototypal inheritance.
* Using classes requires the use of new
* When creating a new instance of a JavaScript class, the new keyword must be used

```javascript
 class Toy {
   ...
}

const myToy1 = Toy(); // throws an error //Uncaught TypeError: Class constructor Toy cannot be invoked without 'new'

const myToy2 = new Toy(); // this works!
```

## Super and Extends

```javascript
 class Tree {
  constructor(size = '10', leaves = {spring: 'green', summer: 'green', fall: 'orange', winter: null}) {
    this.size = size;
    this.leaves = leaves;
    this.leafColor = null;
  }

  changeSeason(season) {
    this.leafColor = this.leaves[season];
    if (season === 'spring') {
      this.size += 1;
    }
  }
}

class Maple extends Tree {
  constructor(syrupQty = 15, size, leaves) {
    super(size, leaves);
    this.syrupQty = syrupQty;
  }

  changeSeason(season) {
    super.changeSeason(season);
    if (season === 'spring') {
      this.syrupQty += 1;
    }
  }

  gatherSyrup() {
    this.syrupQty -= 3;
  }
}

const myMaple = new Maple(15, 5);
myMaple.changeSeason('fall');
myMaple.gatherSyrup();
myMaple.changeSeason('spring');
```

Both Tree and Maple are JavaScript classes. The Maple class is a "subclass" of Tree and uses the extends keyword to set itself as a "subclass". To get from the "subclass" to the parent class, the super keyword is used. Did you notice that super was used in two different ways? In Maple's constructor method, super is used as a function. In Maple's changeSeason() method, super is used as an object!

Using ES5 :/

```javascript
 function Tree(size, leaves) {
  this.size = (typeof size === "undefined")? 10 : size;
  const defaultLeaves = {spring: 'green', summer: 'green', fall: 'orange', winter: null};
  this.leaves = (typeof leaves === "undefined")?  defaultLeaves : leaves;
  this.leafColor;
}

Tree.prototype.changeSeason = function(season) {
  this.leafColor = this.leaves[season];
  if (season === 'spring') {
    this.size += 1;
  }
}

function Maple (syrupQty, size, leaves) {
  Tree.call(this, size, leaves);
  this.syrupQty = (typeof syrupQty === "undefined")? 15 : syrupQty;
}

Maple.prototype = Object.create(Tree.prototype);
Maple.prototype.constructor = Maple;

Maple.prototype.changeSeason = function(season) {
  Tree.prototype.changeSeason.call(this, season);
  if (season === 'spring') {
    this.syrupQty += 1;
  }
}

Maple.prototype.gatherSyrup = function() {
  this.syrupQty -= 3;
}

const myMaple = new Maple(15, 5);
myMaple.changeSeason('fall');
myMaple.gatherSyrup();
myMaple.changeSeason('spring');
```

**super must be called before this**

```javascript
 class Apple {}
class GrannySmith extends Apple {
  constructor(tartnessLevel, energy) {
    this.tartnessLevel = tartnessLevel; // `this` before `super` will throw an error!
    super(energy); 
  }
}
```