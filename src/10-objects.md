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

An arrow function does not define a `this` keyword at all. There is no such thing as `this` in an arrow. If you put a `this` in an arrow, it will behave like any other variable. Therefore it will lexically resolve to some enclosing scope that does define a `this` keyword.

```js
var workshop = {
    teacher: "Sid",
    ask(question) {
        setTimeout( ()=> {
            console.log(this.teacher, question)
        }, 100);
    },
};

workshope.ask("Is this lexical, 'this'?");
// Sid Is this lexical 'this'?
```

This is resolved to the workshop context as that is the call site;

![lexical-this](/img/lexical-this.png)

An arrow function is not a hard bound function. You cannot call `new` on an arrow function. An arrow function is a function that does not define a `this`. If you use nested arrow functions, it will keep resolving upwards until it finds a `this`.

## Resolving this in Arrow Functions

Objects are not scopes. In the following example, the arrow function will look for the `this` context at the global level.

```js
var workshop = {
    teacher: "Sid",
    ask: (question) => {
        console.log(this.teacher, question);
    }
}

workshop.ask("What happened to `this`?");
// undefined What happened to `this`?

workshop.ask.call(workshop, "Still no `this`?");
// undefined Still no `this`?
```

This is a common mistake people have. An arrow function doesn't have `this` and resolves it lexically. There is the scope of the ask function which is an arrow and the global. There is no scope in workshop.

If you need a lexical `this` then an arrow function is the right tool for the job. Otherwise stick with functions.

_If a function uses `this` internally then often you'll bind `this`_.

e.g. in the below example, there is no need to call `this.printRecord.bind(this)` as `printRecord` doesn't actually use `this`.

![this-binding](/img/this-binding.png)

## ES6 class Keyword

The class pattern is the more prevelant pattern used in JS. It is essentially syntactic sugar over the prototype system.

```js
class Workshop {
    constructor(teacher) {
        this.teacher = teacher;
    }
    ask(question) {
        console.log(this.teacher, question);
    }
}

var deepJS = new Workshop("Sid");
var reactJS = new Workshop("Lemmy");

deepJS.ask("Is `class` a class?");
// Sid Is `class` a class?
reachJS.ask("Is this class OK?");
// Lemmy Is this class OK?
```

Classes can be defined with or without an extends clause. The constructor is optional.

If you want to `extend` a class, then you use the `extends` clause, e.g.

```js
class Workshop {
    constructor(teacher) {
        this.teacher = teacher;
    }
    ask(question) {
        console.log(this.teacher, question);
    }
}

class AnotherWorkshop extends Workshop {
    speakUp(msg) {
        this.ask(msg);
    }
}

var JSRecentParts = new AnotherWorkshop("Carl");
JSRecentParts.speakUp("Are classes getting better?");
// Carl Are classes getting better?
```

This is inheritance in classes.

You can also do relative polymorphism. If you have a child class that defines a method of the smae name as a parent class ("Shadowing"), you can refer to the parent from the child by saying `super` e.g.

```js
class Workshop {
    constructor(teacher) {
        this.teacher = teacher;
    }
    ask(question) {
        console.log(this.teacher, question);
    }
}

class AnotherWorkshop extends Workshop {
    ask(msg) {
        super.ask(msg.toUpperCase());
    }
}

var JSRecentParts = new AnotherWorkshop("Carl");
JSRecentParts.speakUp("Are classes super?");
// Carl ARE CLASSES SUPER?
```

This is an example of extension beyond syntactic sugar. Prior to this, there was no way to do relative polymorphism.

Classes are their own complexity sink. They are getting all sorts of their own features, public and private, decorators etc. These are upcoming features.

`this` binding is still affected in classes;

![this-classes](/img/this-classes.png)

A common way people fix this is with the following _PLEASE DO NOT DO THIS_.

![this-classes-hard-bind](/img/this-classes-hard-bind.png)

By doing this you are betraying the system that classes are built upon. The idea of classes is that methods don't exist on your _instances_, but they exist on your _prototypes_.

Favour modules over classes. Use classes if you need super and polymorphism etc.
