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



## The new Keyword

## Default Binding

## Binding Precedence

## Arrow Functions & Lexical this

## Resolving this in Arrow Functions

## ES6 class Keyword

## Fixing this in Classes

