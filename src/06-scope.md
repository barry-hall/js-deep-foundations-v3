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

```js
var teacher = "Kyle";

function otherClass() {
    teacher = "Suzy";
    topic = "React";            // this will ask the global scope for "topic" and global will create it. Here we have essentially created an "auto global"
    console.log("Welcome!");
}

otherClass();   // Welcome!
teacher;        // ?? Suzy, we overwrote the value in the otherClass scope when we invoked the otherClass()
topic;          // ?? React, although if this happened before otherClass() there would be no identifier
```

Never should you _intentionally_ create globals like the above. Always declare them in the appropriate scope.

## Strict Mode

When you use strict mode, (and you should) it will avoid mistakes like creating auto globals. JS doesn't default to strict mode, so you always have to opt in.

```js
"use strict"

var teacher = "Kyle";
function otherClass() {
    teacher = "Suzy";
    topic = "React";            // REFERENCE ERROR!
    console.log("Welcome!");
}

otherClass();
```

Inside of a class and various other ES6 things (like modules) strict mode is assumed.

Strict mode is the future of the language, so you should use it.

## Nested Scope

```js
var teacher = "Kyle";

function otherClass() {
    var teacher = "Suzy";

    function ask(question) {
        console.log(teacher, question)
    }

    ask("Why?");
}

otherClass();           // Suzy, why?
ask("?????");           // Reference error!
```

Here is the scope shown as an image:

![scopes](/img/scope.png)
