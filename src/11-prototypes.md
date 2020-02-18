# Prototypes

Objects are built by "constructors calls" (via `new`). A "constructor call" makes an object "~~based on~~" its own _prototype_. A class is the pattern of a thing. An instance is the concrete thing.

When a "constructor call" makes an object, it's linked to its own prototype.

## Prototypal Class

This is the _old school_ way of creating a prototypal class.

```js
function Workshop(teacher) {
    this.teacher = teacher;
}

Workshop.prototype.ask = function(question) {
    console.log(this.teacher, question);
}

var deepJS = new Workshop("Sid");
var reactJS = new Workshop("Lemmy");

deepJS.ask("Is `prototype` a class?");
// Sid Is `prototype` a class?

reachJS.ask("Isn't `prototype` ugly?");
// Lem Isn't `prototype` ugly?
```

You wouldn't write this type of code anymore, but it's helpful to understand.

## The Prototype Chain

Object.prototype has all the fundamental properties and methods on it. Things like toString etc. Object points to a prototype, which if you called "constructor" on prototype, points back to the object.

![proto-chain](/img/proto-chain.png)

We can share one method with `n` number of instances they are all able to share it because of the `this` binding behavior and prototype linkage. **This is super interesting!**

## Dunder Prototypes

![dunder](/img/dunder.png)

Dunder proto is the `.__proto__` property which is a getter function. This exists up the chain, at something like `object` level within the prototype chain. However, because of `this` binding, the call site on this in the picture is deepJS, therefore the `this` context is deepJS.

## Shadowing Properties

`this` does not work in place of a super. To do so would cause infinite recursion:

![proto-recursion](/img/proto-recursion.png)

If you tries to shadow without class constructs you'd end up with awful code like this:

![proto-shadow](/img/proto-shadow.png)

## Prototypal Inheritance

Prototypal inheritance is essentially object linking:

![proto-inherit](/img/proto-inherit.png)

No matter how far up the chain you have to look for a method, the `this` binding is stil _always the callsite_.

## Classical vs Prototypal Inheritance

In C++ / Java etc when you instantiate an object you are "_copying_" and that class.

![classic-inheritance](/img/proto-classic-inheritance.png)

In prototypal inhertiance, when you instantiate those similar objects they are "_linking_" that initial object.

![proto-inheritance](/img/proto-inheritance.png)

There is an argument that the class design system in JS is just pandering to these "inheritance" concepts that class based language provide. Rather than just embracing what JS already is, using it's dynamic `this` nature. JS is not a class system, but it's getting duct taped to look like one for many.

## Inheritance is Delegation

JavaScript ~~"Inheritance"~~ "Behavior Delegation". That's what JS's prototype system is. It's not a class or inheritance system, it's a delegation system. You can implement a class based system in a prototypal language, but you cannot implement a prototypal system in a class based one.

## OOLO Pattern

_Objects Linked to Other Objects._ Only in JS & Lua can you create an object without a class 🦄 ~~Object~~ Class Oriented Programming.

One proposal for a "new" style is OOLO:

![oloo-delegated](/img/oloo-delegated.png)

## Delegation-Orinted Design

Delegation (Dynamic composition). Using delegation you stop thinking about more traditional "parent > child" and start to think more in terms of "peer to peer". I can have a "LoginController" that is _linked to_ "AuthController".

![delegation-design](/img/delegation-design.png)

Using this style the two objects share a context.

This makes things more testable. For example you can test your LoginFormController by prototype linking to a MockAuthController. You could also make a MockLoginFormController and link to AuthController.
