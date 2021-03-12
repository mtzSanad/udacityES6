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