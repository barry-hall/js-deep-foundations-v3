# Closure

Closure is one of the most important things in computer science. It's one of the most prevelant concepts in all of programming.

## Origin of Closure

Closure originates from lambda calculus.

## What is Closure

Closure is when a function is able to remember and access it's lexical scope even when that function executes outside that lexical scope.

Closure is the preservation and linkage back to the original scope of where it was defined no matter where you pass that value or it executes. It preserves that scope.

Some examples:

```js
function ask(question) {
    return function holdYourQuestion() {
        console.log(question);
    };
}

var myQuestion = ask("what is closure?");

myQuestion(); // What is closure?

```

Here as you are return a function that is _closed over the question variable_ then even though the `ask` function has finished, we still have access to that variable.

## Closing Over Variables

```js
var teacher = "Kyle";

var myTeacher = function() {
    console.log(teacher);
};

teacher = "Suzy";

myTeacher();        // "Suzy"
```

It's Suzy because we closed over the variable `teacher`. You can't close over a value. Only a variable.

Don't think of Closure as capturing values, think of it as preserving access to variables.

```js
for(var i = 1; i <= 3; i++) {
    setTimeout(function() {
        console.log(`i: ${i}`);
    }, i * 1000);
}

// i: 4
// i: 4
// i: 4
```

To fix this you would create a block scoped declaration.

```js
for(var i = 1; i <= 3; i++) {
    let j = i;
    setTimeout(function() {
        console.log(`j: ${j}`);
    }, j * 1000);
}

// i: 1
// i: 2
// i: 3
```

Now `let j` is going to run everytime the for loop iterates and is going to make a whole new `j` in each iteration of the loop. When we close over this, we are closing over a whole new `j`. As they are all seperate, we get whole new values. This is the thing with closure, close over a _variable_ and not a _value_.

The point is that if you need multiple different values being closed over you need multiple different variables. You need to close over different variables, _not_ try to capture values.

In ES6 they introduced `let` into the forloop. Which gives a brand new `i` for each iteration, resulting in...

```js
for(let i = 1; i <= 3; i++) {
    setTimeout(function() {
        console.log(`i: ${i}`);
    },i * 1000);
}
// i: 1
// i: 2
// i: 3
```

Here the closure _magically_ just works.

## Module Pattern

_The module pattern is not_...

```js
var workshop = {
    teacher: "Sid",
    ask(question) {
        console.log(this.teacher,question);
    }
}

workshop.ask("Is this a module?");
//Sid Is this a module?
```

A common pattern where you have a set of behaviour and a set of data is to group this together as an object. This is the _namespace_ pattern. It is effectively collecting them into a namespace. This was a common pattern for years. There is nothing wrong with this, however, it is 100% not a module. The module pattern requires the concept of _incapsuation_. Hiding the data and the behaviour. Think of _information hiding_.

The idea of a module is that there are things that are _public_—the API—and things that are private, that no-one can touch.

> **Modules _encapsulate_ data and behaviour (methods) together. The state (data) of a module is held by its methods via closure.**

```js
var workshop = (function Module(teacher) {
    var publicAPI = {ask, };
    return publicAPI

    // ***********
    function ask(question) {
        console.log(teacher, question);
    }
})("Sid");

workshop.ask("It's a mdoule, right?");
// Sid It's a module, right?
```

^ This was the first example of the module pattern. We have an _outer_ encolosing function (an IIFE) The closure prevents the scope from going away. We then have a second component, an inner function, that is closed over those variables. Since it's closed over, the workshop object on the outside that has reference to that inner function is preserving the inner scope through closure. This pattern would allow me to have lots of private methods and state, yet we only expose what's in the public api object. This pattern is a singleton. It's always the same object.

If you have a "module" that doesn't have any state that changes, you have an overengineered namespace.

The purpose of a module is that you have some state that you are closed over and you are controlling access to it over a minimal public api.

Factory function example;

```js
function WorkshopModule(teacher) {
    var publicAPI = {ask, };
    return publicAPI;

    function ask(questions) {
        console.log(teacher, question);
    }
};

var workshop = WorkshopModule("Sid");
workshop.ask("It's a module, right?");

// Sid It's a module, right?
```

Factory function can be called hundred of times, each time you will get a seperate instance with it's own state that doesn't mix with one another.

**The module pattern is the most important of all JS code organisation patterns.**

## ES6 Modules & Node.js

There was clamouring that if modules were so important as a design pattern for JS, then we ought to have first class syntactic support for them.

ES6 introduced modules.

```js
var teacher = "Sid";

export default function ask(question) {
    console.log(teacher, question)
};
```

Anything you export is public, everything you don't, is private. Modules are file based and singletons. You cannot import it more than once. If you want someone to have multiple instances of your module code, you need to expose a factory function for them to use.

## ES6 Module Syntax

There are two major styles of importing modules. A "Java" style import or a "namespace" import.

```js
import ask from "workshop.mjs"

ask("It's a default import, right?");
// Sid It's a default import, right?

import * as workshop from "workshop.mjs"

workshop.ask("It's a namespace import, right?");
// Sid It's a namespace import, right?
```

**You're organising a set of behviour into a cohesive unit, hiding data in it and exposing a minimal api.**
