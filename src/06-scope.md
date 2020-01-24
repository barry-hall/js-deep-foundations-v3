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

Scope is "author" time decisions.

## Executing Code

`var teacher =  "Kyle"`. The compiler handles _var teacher_ and the execution engine handles _teacher = "Kyle"_.

When you reference a variable in a source position or a target position you first have to look it up. The relevent scopes are checked for them and the reference returned first. Source and target positions are created at compile time, but we don't use them until runtime.

## Code Execution: Finishing Up

A source reference is where you are requesting the value of something. A target reference is where you are assigning. eg:

```js
var question = "Why"?; // < Target reference for an identifier called "question".
console.log(question)  // < a Source reference to question.
```

## Dynamic Global Variables

