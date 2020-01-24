# Scope and Function Expressions

## Function Expressions

* Function ***declarations*** attach themselves to the enclosing scope
* Function ***expressions*** attach themselves to their own scope

```js
function teacher() { /* .. */}              // Declaration

var myTeacher = function anotherTeacher() { // Expression
    console.log(anotherTeacher);
}

console.log(teacher);
console.log(myTeacher);
console.log(anotherTeacher); //REFERENCE ERROR! (it has it's own scope)
```

There is a difference in what can happen at compile time vs run time. Here, "anoterTeacher" will be assigned to the scope of what would be in "myTeacher".

Named function expressions: "a function expression that has been given a name"

Something is a function delcaration if the word function is the first thing in the statement. If it's _not_ the first thing (eg, if a variable or operator etc), it's an expression.

```js
var clickHandller = function() { // <- this is an anonymous function expression
    // ..
}

var keyHandler = function keyHandler() { // <- this is a named function expression
    // ..
}
```

> You should 100% of the time _prefer_ the named function expression over the anonymous function expression.

## Naming Function Expressions

Some key reasons you should favour naming your function expressions:

1. Reliable function self-reference (recurion, etc)
2. More debuggable stack traces
3. More self-documenting code

Prefer function delcarations with names. If you are going to use an expression, give it a name.

## Arrow Functions

```js
var ids = people.map(person => person.id);      // Arrow function

var ids = people.map(function getId(person)){   // Anonymous arrow function
    return person.id;
}
```

## Functions Types Hierarchy
