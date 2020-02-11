# Objects

Objects(Oriented)

* this
* class {}
* Prototypes
* Inheritance vs Behavior Delegation ( OO vs. OLOO )

## The this Keyword

The most perpetually confused of all JS features.

> A  function's _this_ references the exectuion context for that call, determind entirely by **how the function was called**.

additionally;

> A _this_-aware function can thud have a different context each time it's called, which makes it more flexible & reusable.

`this` essentially enables dynamic scope.

![this-context](/img/this-context.png)

In the example, we are saying "use this particular object as your 'this' keyword and invoke the function in that context".

`this` exists so that we can invoke functions in different contexts.

There are four different ways to invoke a function. Each one of them answers the `this` keyword differently.

## Implicit & Explicit Binding

Implicit binding the `this` keyword is interpreted from the call site, in the blow examples, this is the "workshop".

![implicit-this](/img/implicit-this.png)

dynamic binding -> Sharing

![dynamic-binding](/img/dynamic-binding.png)

The `call` keyword can be used on a function, who's first argument is an object to which `this` needs to refer to.

"Invoked the ask function with the context of `workshop1`"

![call-example](/img/call-example.png)

In the below example, line 8 the context would be the window or global, as that is the executing context of the callback that is being fired which is passed into the setTimeout method.

[!hard-binding](/img/hard-binding.png)

Bind will take away any flexibility of scope and force the funciton to run in the context that it is bound to. Invoke this function and no matter how you invoke it always use `workshop` as `this` context.

***bind doesn't invoke the function, it produces a new function that is bound a particular specific `this` context.***

## The new Keyword

The new keyword creates what's called a "constructor call" it does four specific things.

```js
function ask(question) {
    console.log(this.teacher, question);
}

var newEmptyObject = new ask("What is `new` doing here?");
// undefined What is `new` doing here?
```

The purpose of the new keyword is to invoke a function with the `this` keyword pointing at a new empty object. In theory you could achieve the same with `function.call({}, "what is...")` as you are passing a new empty object to this `this` binding.

***The `new` keyword:***

* Create a brand new empty object
* Link that object to another object
* Call function with `this` set to the new object
* If function does not return an object; assume return of `this`

## Default Binding

The final way of invoking a function is called default binding.

```js
var teacher = "Sid";

function ask(question) {
    console.log(this.teacher, question);
}

function askAgain(question) {
    "use strict";
    console.log(this.teacher, question);
}

ask("What's the non-strict-mode default?");
// Sid What's the non-strict-mode default?
askAgain("What's the strict-mode default?");
// TypeError
```

In non strict mode, the default function call falls back to the global context. In strict mode, when you invoke it with no other `this` bindings, the default is to leave `this` undefined. Hence the type error in `askAgain`.

## Binding Precedence

Take the following code:

```js
var workshop = {
    teacher: "Sid",
    ask: function ask(question) {
        console.log(this.teacher, question);
    },
};

new (workshope.ask.bin(workshop))("What does this do?");
```

Here we have a new keyword, context object and a bind. There are three of the four rules matched on the same callsight for invoking the function.

If more than one rule matches a call site, the order of precedence is:

1. Is the function called by `new`?
2. Is the function called by `call()` or `apply()`?
3. Is the function called on a context object?
4. DEFAULT: global object (except strict mode)

## Arrow Functions & Lexical this



## Resolving this in Arrow Functions



## ES6 class Keyword



## Fixing this in Classes

