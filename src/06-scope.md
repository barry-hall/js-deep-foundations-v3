# Scope

Scope:

* Nested Scope
* Hoisting
* Closure
* Modules

> Scope is where to look for things...

```js
x = 42;
console.log(y);
```

All variables are receiving the assignment, or you are retrieving the value from the variable.

JavsScript organizes scopes with _functions_ and blocks.

## Compilation & Scope

Scope will have multiple levels and assignments:

```js
var teacher = "Kyle";           //SCOPE Identifier 1

function otherClass() {         //SCOPE Identifier 1
    var teacher = "Suzy";       //SCOPE Identifier 2
    console.log("Welcome!");
}

function ask() {                //SCOPE Identifier 1
    var question = "Why?";      //SCOPE Identifier 3 (2 being "teacher" in otherClass)
    console.log(question);
}

otherClass();   // Welcome!
ask();          // Why?
```

## Executing Code
