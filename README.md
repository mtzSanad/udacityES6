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

# Built-ins

## Symbols

Primative data types are

* Numbers
* Strings
* null
* undefined
* boolean  
* Symbol - ES6

A symbol is a unique and immutable data type that is often used to identify object properties.

To create a symbol, you write Symbol() with an optional string as its description.

```javascript
const sym1 = Symbol('apple');
console.log(sym1);
```

This will create a unique symbol and store it in sym1. The description "apple" is just a way to describe the symbol, but it can’t be used to access the symbol itself.

```javascript
const sym2 = Symbol('banana');
const sym3 = Symbol('banana');
console.log(sym2 === sym3); //false
```

…then the result is false because the description is only used to describe the symbol. It’s not used as part of the symbol itself—each time a new symbol is created, regardless of the description.

```javascript
const bowl = {
  'apple': { color: 'red', weight: 136.078 },
  'banana': { color: 'yellow', weight: 183.151 },
  'orange': { color: 'orange', weight: 170.097 },
  'banana': { color: 'yellow', weight: 176.845 }
};
console.log(bowl);
//Object {apple: Object, banana: Object, orange: Object}
```

Instead of adding another banana to the bowl, our previous banana is overwritten by the new banana being added to the bowl. To fix this problem, we can use symbols.

```javascript
const bowl = {
  [Symbol('apple')]: { color: 'red', weight: 136.078 },
  [Symbol('banana')]: { color: 'yellow', weight: 183.15 },
  [Symbol('orange')]: { color: 'orange', weight: 170.097 },
  [Symbol('banana')]: { color: 'yellow', weight: 176.845 }
};
console.log(bowl);
//Object {Symbol(apple): Object, Symbol(banana): Object, Symbol(orange): Object, Symbol(banana): Object}
```

## Iterable Protocol

* the iterable protocol
* the iterator protocol

**The Iterable Protocol**

The iterable protocol is used for defining and customizing the iteration behavior of objects. What that really means is you now have the flexibility in ES6 to specify a way for iterating through values in an object. For some objects, they already come built-in with this behavior. For example, strings and arrays are examples of built-in iterables.

```javascript
const digits = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9];
for (const digit of digits) {
  console.log(digit);
}
```

If you recall from earlier lesson 1, any object that is iterable can use the new for...of loop. Later in this lesson, you’ll also learn about Sets and Maps which are other examples of built-in iterables.

How it Works

In order for an object to be iterable, it must implement the iterable interface. If you come from a language like Java or C, then you’re probably familiar with interfaces, but for those of you who aren’t, that basically means that in order for an object to be iterable it must contain a default iterator method. This method will define how the object should be iterated.

The iterator method, which is available via the constant [Symbol.iterator], is a zero arguments function that returns an iterator object. An iterator object is an object that conforms to the iterator protocol.

The Iterator Protocol

The iterator protocol is used to define a standard way that an object produces a sequence of values. What that really means is you now have a process for defining how an object will iterate. This is done through implementing the .next() method.

How it Works
An object becomes an iterator when it implements the .next() method. The .next() method is a zero arguments function that returns an object with two properties:

value : the data representing the next value in the sequence of values within the object
done : a boolean representing if the iterator is done going through the sequence of values
If done is true, then the iterator has reached the end of its sequence of values.
If done is false, then the iterator is able to produce another value in its sequence of values.

```javascript
const digits = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9];
const arrayIterator = digits[Symbol.iterator]();

console.log(arrayIterator.next());
console.log(arrayIterator.next());
console.log(arrayIterator.next());
// Object {value: 0, done: false}
// Object {value: 1, done: false}
// Object {value: 2, done: false}
```

## Sets

If you think back to mathematics, a set is a collection of distinct items. For example, {2, 4, 5, 6} is a set because each number is unique and appears only once. However, {1, 1, 2, 4} is not a set because it contains duplicate entries (the 1 is in there more than once!).

In ES6, there’s a new built-in object that behaves like a mathematical set and works similarly to an array. This new object is conveniently called a "Set". The biggest differences between a set and an array are:

Sets are not indexed-based - you do not refer to items in a set based on their position in the set
items in a Set can’t be accessed individually
Basically, a Set is an object that lets you store unique items. You can add items to a Set, remove items from a Set, and loop over a Set. These items can be either primitive values or objects.

```javascript
const games = new Set();
console.log(games); //Set {}

const games = new Set(['Super Mario Bros.', 'Banjo-Kazooie', 'Mario Kart', 'Super Mario Bros.']);
console.log(games);
//Set {'Super Mario Bros.', 'Banjo-Kazooie', 'Mario Kart'} Duplication is removed

//Modifying
const games = new Set(['Super Mario Bros.', 'Banjo-Kazooie', 'Mario Kart', 'Super Mario Bros.']);

games.add('Banjo-Tooie');
games.add('Age of Empires');
games.delete('Super Mario Bros.');

console.log(games);
//Set {'Banjo-Kazooie', 'Mario Kart', 'Banjo-Tooie', 'Age of Empires'}

games.clear()
console.log(games);
//Set {}
```

>TIP: If you attempt to .add() a duplicate item to a Set, you won’t receive an error, but the item will not be added to the Set. Also, if you try to .delete() an item that is not in a Set, you won’t receive an error, and the Set will remain unchanged.

>.add() returns the Set if an item is successfully added. On the other hand, .delete() returns a Boolean (true or false) depending on successful deletion.

```javascript
const months = new Set(['January', 'February', 'March', 'April', 'May', 'June', 'July', 'August', 'September', 'October', 'November', 'December']);
console.log(months.size);
```

Remember, Sets can’t be accessed by their index like an array, so you use the .size property instead of .length property to get the size of the Set.

Checking item existance
```javascript
console.log(months.has('September')); //true or false
console.log(months.values()); // getting all values
```

>TIP: The .keys() method will behave the exact same way as the .values() method by returning the values of a Set within a new Iterator Object. The .keys() method is an alias for the .values() method for similarity with maps. You’ll see the .keys() method later in this lesson during the Maps section.

Iterating through sets

```javascript
const iterator = months.values();
iterator.next();

//OR

const colors = new Set(['red', 'orange', 'yellow', 'green', 'blue', 'violet', 'brown', 'black']);
for (const color of colors) {
  console.log(color);
}
```

## WeakSet

A WeakSet is just like a normal Set with a few key differences:

1- a WeakSet can only contain objects
2- a WeakSet is not iterable which means it can’t be looped over
3- a WeakSet does not have a .clear() method

```javascript
let student1 = { name: 'James', age: 26, gender: 'male' };
let student2 = { name: 'Julia', age: 27, gender: 'female' };
let student3 = { name: 'Richard', age: 31, gender: 'male' };

const roster = new WeakSet([student1, student2, student3]);
console.log(roster);

roster.add('Amanda');// Uncaught TypeError: Invalid value used in weak set(…)
```
Why WeakSet?

Garbage Collection
In JavaScript, memory is allocated when new values are created and is "automatically" freed up when those values are no longer needed. This process of freeing up memory after it is no longer needed is what is known as garbage collection.

WeakSets take advantage of this by exclusively working with objects. If you set an object to null, then you’re essentially deleting the object. And when JavaScript’s garbage collector runs, the memory that object previously occupied will be freed up to be used later in your program.

```javascript
student3 = null;
console.log(roster);

//WeakSet {Object {name: 'Julia', age: 27, gender: 'female'}, Object {name: 'James', age: 26, gender: 'male'}}
```

What makes this so useful is you don’t have to worry about deleting references to deleted objects in your WeakSets, JavaScript does it for you! When an object is deleted, the object will also be deleted from the WeakSet when garbage collection runs. This makes WeakSets useful in situations where you want an efficient, lightweight solution for creating groups of objects.

## Maps

If Sets are similar to Arrays, then Maps are similar to Objects because Maps store key-value pairs similar to how objects contain named properties with values.

Essentially, a Map is an object that lets you store key-value pairs where both the keys and the values can be objects, primitive values, or a combination of the two.

```javascript
const employees = new Map();
console.log(employees);
//Map {}
```

Unlike Sets, you can’t create Maps from a list of values; instead, you add key-values by using the Map’s .set() method.

```javascript
const employees = new Map();

employees.set('james.parkes@udacity.com', { 
    firstName: 'James',
    lastName: 'Parkes',
    role: 'Content Developer' 
});
employees.set('julia@udacity.com', {
    firstName: 'Julia',
    lastName: 'Van Cleve',
    role: 'Content Developer'
});
employees.set('richard@udacity.com', {
    firstName: 'Richard',
    lastName: 'Kalehoff',
    role: 'Content Developer'
});

console.log(employees);

employees.delete('julia@udacity.com');
employees.delete('richard@udacity.com');
console.log(employees);

employees.clear()
console.log(employees);

const members = new Map();

members.set('Evelyn', 75.68);
members.set('Liam', 20.16);
members.set('Sophia', 0);
members.set('Marcus', 10.25);

console.log(members.has('Xavier'));
console.log(members.has('Marcus'));
//Looping

let iteratorObjForKeys = members.keys();
iteratorObjForKeys.next();

for (const member of members) {
  console.log(member);
}

members.forEach((value, key) => console.log(key, value));
```

What is a WeakMap?
A WeakMap is just like a normal Map with a few key differences:

a WeakMap can only contain objects as keys,
a WeakMap is not iterable which means it can’t be looped and
a WeakMap does not have a .clear() method.

```javascript
const book1 = { title: 'Pride and Prejudice', author: 'Jane Austen' };
const book2 = { title: 'The Catcher in the Rye', author: 'J.D. Salinger' };
const book3 = { title: 'Gulliver’s Travels', author: 'Jonathan Swift' };

const library = new WeakMap();
library.set(book1, true);
library.set(book2, false);
library.set(book3, true);

console.log(library);

library.set('The Grapes of Wrath', false); //error

book1 = null;
console.log(library);
```

>TIP: If you .set() a key-value pair to a Map that already uses the same key, you won’t receive an error, but the key-value pair will overwrite what currently exists in the Map. Also, if you try to .delete() a key-value that is not in a Map, you won’t receive an error, and the Map will remain unchanged.

>The .delete() method returns true if a key-value pair is successfully deleted from the Map object, and false if unsuccessful. The return value of .set() is the Map object itself if successful.

## Promises

Promises
A JavaScript Promise is created with the new Promise constructor function - new Promise(). A promise will let you start some work that will be done asynchronously and let you get back to your regular work. When you create the promise, you must give it the code that will be run asynchronously. You provide this code as the argument of the constructor function:

```javascript
new Promise(function () {
    window.setTimeout(function createSundae(flavor = 'chocolate') {
        const sundae = {};
        // request ice cream
        // get cone
        // warm up ice cream scoop
        // scoop generous portion into cone!
    }, Math.random() * 2000);
});
```

This code creates a promise that will start in a few seconds after I make the request. Then there are a number of steps that need to be made in the createSundae function.

Indicated a Successful Request or a Failed Request
But once that's all done, how does JavaScript notify us that it's finished and ready for us to pick back up? It does that by passing two functions into our initial function. Typically we call these resolve and reject.

The function gets passed to the function we provide the Promise constructor - typically the word "resolve" is used to indicate that this function should be called when the request completes successfully. Notice the resolve on the first line:

```javascript
new Promise(function (resolve, reject) {
    window.setTimeout(function createSundae(flavor = 'chocolate') {
        const sundae = {};
        // request ice cream
        // get cone
        // warm up ice cream scoop
        // scoop generous portion into cone!
        resolve(sundae);
    }, Math.random() * 2000);
});
```

Now when the sundae has been successfully created, it calls the resolve method and passes it the data we want to return - in this case the data that's being returned is the completed sundae. So the resolve method is used to indicate that the request is complete and that it completed successfully.

If there is a problem with the request and it couldn't be completed, then we could use the second function that's passed to the function. Typically, this function is stored in an identifier called "reject" to indicate that this function should be used if the request fails for some reason. Check out the reject on the first line:

```javascript
new Promise(function (resolve, reject) {
    window.setTimeout(function createSundae(flavor = 'chocolate') {
        const sundae = {};
        // request ice cream
        // get cone
        // warm up ice cream scoop
        // scoop generous portion into cone!
        if ( /* iceCreamConeIsEmpty(flavor) */ ) {
            reject(`Sorry, we're out of that flavor :-(`);
        }
        resolve(sundae);
    }, Math.random() * 2000);
});
```

So the reject method is used when the request could not be completed. Notice that even though the request fails, we can still return data - in this case we're just returning text that says we don't have the desired ice cream flavor.

A Promise constructor takes a function that will run and then, after some amount of time, will either complete successfully (using the resolve method) or unsuccessfully (using the reject method). When the outcome has been finalized (the request has either completed successfully or unsuccessfully), the promise is now fulfilled and will notify us so we can decide what to do with the response.

**Promises Return Immediately**
The first thing to understand is that a Promise will immediately return an object.

```javascript
const myPromiseObj = new Promise(function (resolve, reject) {
    // sundae creation code
});
```

That object has a .then() method on it that we can use to have it notify us if the request we made in the promise was either successful or failed. The .then() method takes two functions:

the function to run if the request completed successfully
the function to run if the request failed to complete

```javascript
mySundae.then(function(sundae) {
    console.log(`Time to eat my delicious ${sundae}`);
}, function(msg) {
    console.log(msg);
    self.goCry(); // not a real method
});
```

As you can see, the first function that's passed to .then() will be called and passed the data that the Promise's resolve function used. In this case, the function would receive the sundae object. The second function will be called and passed the data that the Promise's reject function was called with. In this case, the function receives the error message "Sorry, we're out of that flavor :-(" that the reject function was called with in the Promise code above.

> Promises details course https://classroom.udacity.com/courses/ud898

## Proxies

To create a proxy object, we use the Proxy constructor - new Proxy();. The proxy constructor takes two items:

the object that it will be the proxy for
an object containing the list of methods it will handle for the proxied object

The second object is called the handler.

A Pass Through Proxy
The simplest way to create a proxy is to provide an object and then an empty handler object.

```javascript
var richard = {status: 'looking for work'};
var agent = new Proxy(richard, {});

agent.status; // returns 'looking for work'
```
The above doesn't actually do anything special with the proxy - it just passes the request directly to the source object! If we want the proxy object to actually intercept the request, that's what the handler object is for!

The key to making Proxies useful is the handler object that's passed as the second object to the Proxy constructor. The handler object is made up of a methods that will be used for property access. Let's look at the get:

```javascript
const richard = {status: 'looking for work'};
const handler = {
    get(target, propName) {
        console.log(target); // the `richard` object, not `handler` and not `agent`
        console.log(propName); // the name of the property the proxy (`agent` in this case) is checking
    }
};
const agent = new Proxy(richard, handler);
agent.status; // logs out the richard object (not the agent object!) and the name of the property being accessed (`status`)
```

In the code above, the handler object has a get method (called a "trap" since it's being used in a Proxy). When the code agent.status; is run on the last line, because the get trap exists, it "intercepts" the call to get the status property and runs the get trap function. This will log out the target object of the proxy (the richard object) and then logs out the name of the property being requested (the status property). And that's all it does! It doesn't actually log out the property! This is important - if a trap is used, you need to make sure you provide all the functionality for that specific trap.

```javascript
const richard = {status: 'looking for work'};
const handler = {
    get(target, propName) {
        console.log(target);
        console.log(propName);
        return target[propName];
    }
};
const agent = new Proxy(richard, handler);
agent.status; // (1)logs the richard object, (2)logs the property being accessed, (3)returns the text in richard.status
```
Notice we added the return target[propName]; as the last line of the get trap. This will access the property on the target object and will return it.

Having the proxy return info, directly
Alternatively, we could use the proxy to provide direct feedback:


```javascript
const richard = {status: 'looking for work'};
const handler = {
    get(target, propName) {
        return `He's following many leads, so you should offer a contract as soon as possible!`;
    }
};
const agent = new Proxy(richard, handler);
agent.status; // returns the text `He's following many leads, so you should offer a contract as soon as possible!`
```

With this code, the Proxy doesn't even check the target object, it just directly responds to the calling code.

So the get trap will take over whenever any property on the proxy is accessed. If we want to intercept calls to change properties, then the set trap needs to be used!

The set trap is used for intercepting code that will change a property. The set trap receives: the object it proxies the property that is being set the new value for the proxy

```javascript
const richard = {status: 'looking for work'};
const handler = {
    set(target, propName, value) {
        if (propName === 'payRate') { // if the pay is being set, take 15% as commission
            value = value * 0.85;
        }
        target[propName] = value;
    }
};
const agent = new Proxy(richard, handler);
agent.payRate = 1000; // set the actor's pay to $1,000
agent.payRate; // $850 the actor's actual pay
```
In the code above, notice that the set trap checks to see if the payRate property is being set. If it is, then the proxy (the agent) takes 15 percent off the top for her own commission! Then, when the actor's pay is set to one thousand dollars, since the payRate property was used, the code took 15% off the top and set the actual payRate property to 850;

Other Traps
So we've looked at the get and set traps (which are probably the ones you'll use most often), but there are actually a total of 13 different traps that can be used in a handler!

the get trap - lets the proxy handle calls to property access
the set trap - lets the proxy handle setting the property to a new value
the apply trap - lets the proxy handle being invoked (the object being proxied is a function)
the has trap - lets the proxy handle the using in operator
the deleteProperty trap - lets the proxy handle if a property is deleted
the ownKeys trap - lets the proxy handle when all keys are requested
the construct trap - lets the proxy handle when the proxy is used with the new keyword as a constructor
the defineProperty trap - lets the proxy handle when defineProperty is used to create a new property on the object
the getOwnPropertyDescriptor trap - lets the proxy handle getting the property's descriptors
the preventExtenions trap - lets the proxy handle calls to Object.preventExtensions() on the proxy object
the isExtensible trap - lets the proxy handle calls to Object.isExtensible on the proxy object
the getPrototypeOf trap - lets the proxy handle calls to Object.getPrototypeOf on the proxy object
the setPrototypeOf trap - lets the proxy handle calls to Object.setPrototypeOf on the proxy object
As you can see, there are a lot of traps that let the proxy manage how it handles calls back and forth to the proxied object.

Initially, it can be a bit unclear as to why proxies are all that beneficial when there are already getter and setter methods provided in ES5. With ES5's getter and setter methods, you need to know before hand the properties that are going to be get/set:

```javascript
var obj = {
    _age: 5,
    _height: 4,
    get age() {
        console.log(`getting the "age" property`);
        console.log(this._age);
    },
    get height() {
        console.log(`getting the "height" property`);
        console.log(this._height);
    }
};
```

But look what happens when we now add a new property to the object:

```javascript
obj.weight = 120; // set a new property on the object
obj.weight; // logs just 120
```

with ES6 proxy

```javascript
const proxyObj = new Proxy({age: 5, height: 4}, {
    get(targetObj, property) {
        console.log(`getting the ${property} property`);
        console.log(targetObj[property]);
    }
});

proxyObj.age; // logs 'getting the age property' & 5
proxyObj.height; // logs 'getting the height property' & 4
```

A proxy object sits between a real object and the calling code. The calling code interacts with the proxy instead of the real object. To create a proxy:

use the new Proxy() constructor
pass the object being proxied as the first item
the second object is a handler object
the handler object is made up of 1 of 13 different "traps"
a trap is a function that will intercept calls to properties let you run code
if a trap is not defined, the default behavior is sent to the target object
Proxies are a powerful new way to create and manage the interactions between objects.

## Generators

Whenever a function is invoked, the JavaScript engine starts at the top of the function and runs every line of code until it gets to the bottom. There's no way to stop the execution of the function in the middle and pick up again at some later point. This "run-to-completion" is the way it's always been:

```javascript
function getEmployee() {
    console.log('the function has started');

    const names = ['Amanda', 'Diego', 'Farrin', 'James', 'Kagure', 'Kavita', 'Orit', 'Richard'];

    for (const name of names) {
        console.log(name);
    }

    console.log('the function has ended');
}

getEmployee();
//output
// the function has started
// Amanda
// Diego
// Farrin
// James
// Kagure
// Kavita
// Orit
// Richard
// the function has ended
```

ut what if you want to print out the first 3 employee names then stop for a bit, then, at some later point, you want to continue where you left off and print out more employee names. With a regular function, you can't do this since there's no way to "pause" a function in the middle of its execution

Pausable Functions
If we _do_ want to be able to pause a function mid-execution, then we'll need a new type of function available to us in ES6 - generator functions! Let's look at one:

```javascript
function* getEmployee() {
    console.log('the function has started');

    const names = ['Amanda', 'Diego', 'Farrin', 'James', 'Kagure', 'Kavita', 'Orit', 'Richard'];

    for (const name of names) {
        console.log( name );
    }

    console.log('the function has ended');
}
```

Notice the asterisk (i.e. *) right after the function keyword? That asterisk indicates that this function is actually a generator!

Now check out what happens when we try running this function:

```javascript
getEmployee();

// this is the response I get in Chrome:
getEmployee {[[GeneratorStatus]]: "suspended", [[GeneratorReceiver]]: Window}
```

When a generator is invoked, it doesn't actually run any of the code inside the function. Instead, it creates and returns an iterator. This iterator can then be used to execute the actual generator's inner code.

```javascript
const generatorIterator = getEmployee();
generatorIterator.next();

//output
// the function has started
// Amanda
// Diego
// Farrin
// James
// Kagure
// Kavita
// Orit
// Richard
// the function has ended
```

Now if you tried the code out for yourself, the first time the iterator's .next() method was called it ran all of the code inside the generator. Did you notice anything? The code never paused! So how do we get this magical, pausing functionality?

The Yield Keyword
The yield keyword is new and was introduced with ES6. It can only be used inside generator functions. yield is what causes the generator to pause. Let's add yield to our generator and give it a try:

```javascript
function* getEmployee() {
    console.log('the function has started');

    const names = ['Amanda', 'Diego', 'Farrin', 'James', 'Kagure', 'Kavita', 'Orit', 'Richard'];

    for (const name of names) {
        console.log(name);
        yield;
    }

    console.log('the function has ended');
}
```

Notice that there's now a yield inside the for...of loop. If we invoke the generator (which produces an iterator) and then call .next(), we'll get the following output:

Yielding Data to the "Outside" World
Instead of logging the names to the console and then pausing, let's have the code "return" the name and then pause.

```javascript
function* getEmployee() {
    console.log('the function has started');

    const names = ['Amanda', 'Diego', 'Farrin', 'James', 'Kagure', 'Kavita', 'Orit', 'Richard'];

    for (const name of names) {
        yield name;
    }

    console.log('the function has ended');
}

const generatorIterator = getEmployee();
let result = generatorIterator.next();
result.value // is "Amanda"

generatorIterator.next().value // is "Diego"
generatorIterator.next().value // is "Farrin"

```

```javascript
function* getEmployee() {
    const names = ['Amanda', 'Diego', 'Farrin', 'James', 'Kagure', 'Kavita', 'Orit', 'Richard'];
    const facts = [];

    for (const name of names) {
        // yield *out* each name AND store the returned data into the facts array
        facts.push(yield name); 
    }

    return facts;
}

const generatorIterator = getEmployee();

// get the first name out of the generator
let name = generatorIterator.next().value;

// pass data in *and* get the next name
name = generatorIterator.next(`${name} is cool!`).value; 

// pass data in *and* get the next name
name = generatorIterator.next(`${name} is awesome!`).value; 

// pass data in *and* get the next name
name = generatorIterator.next(`${name} is stupendous!`).value; 

// you get the idea
name = generatorIterator.next(`${name} is rad!`).value; 
name = generatorIterator.next(`${name} is impressive!`).value;
name = generatorIterator.next(`${name} is stunning!`).value;
name = generatorIterator.next(`${name} is awe-inspiring!`).value;

// pass the last data in, generator ends and returns the array
const positions = generatorIterator.next(`${name} is magnificent!`).value; 

// displays each name with description on its own line
positions.join('\n'); 
```

# Developer-Fu

Code doesn't work in old browsers
The code we've been looking at in this course is not supported by older browsers. Older browsers that were developed prior to the release of ES6 were developed to support the version of JavaScript at the time (which was ES5.1). If you try running any ES6 code in an older browser, it won't work.

Compatability table http://kangax.github.io/compat-table/es6/

What is a polyfill?
A polyfill, or polyfiller, is a piece of code (or plugin) that provides the technology that you, the developer, expect the browser to provide natively.

An example polyfill
The code below is a polyfill for the new ES6 String method, startsWith():

```javascript
if (!String.prototype.startsWith) {
  String.prototype.startsWith = function (searchString, position) {
    position = position || 0;
    return this.substr(position, searchString.length) === searchString;
  };
}
```

The most popular JavaScript transpiler is called Babel.

Babel's original name was slightly more descriptive - 6to5. This was because, originally, Babel converted ES6 code to ES5 code. Now, Babel does a lot more. It'll convert ES6 to ES5, JSX to JavaScript, and Flow to JavaScript.

Before we look at transpiling code on our computer, let's do a quick test by transpiling some ES6 code into ES5 code directly on the Babel website. Check out Babel's REPL and paste the following code into the section on the left: