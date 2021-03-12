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