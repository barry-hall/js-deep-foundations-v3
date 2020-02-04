# Advanced Scope

## Lexical and Dynamic Scope

**Lexical scope**: The compiler working out scopes ahead of time before being executed. This is the author time decision to put functions and variables in their chosen scope.

Most programming languages are lexically scoped.

**dyanmic scope**: it does exist, most commonly seen in bash script. Bash is not compiled at all.

## Lexical Scope

!["lexical scope"](/img/lexical-scope.png)

Lexical scope is popular as you can easily do optimisation. You can create your scopes at design time, you don't have to work them out at runtime.

## Dynamic Scope

If dynamic scoping _did_ exist in JavaScript, it would look like the following; _note this entirely theoretical_.

!["dynamic scope"](/img/dynamic-scope.png)

## Function Scoping

Take the following example;

```js
var teacher = "Kyle";
// ..
var teacher = "Suzy";
console.log(teacher); // Suzy
// ..
console.log(teacher); // Suzy -- oops!
```

The problem isn't the variable can be reassigned, but that we have a naming collision.

To resolve this problem, we can use function scoping:

```js
var teacher = "Kyele";

function anotherTeacher() {
    var teacher = "Suzy";
    console.log(teacher);   // Suzy
}

anotherTeacher();

console.log(teacher);   // Kyle
```

^ this is just moving things around a little. If we _really_ wanted to control the scope then we could use something like and IIFE (see below).

There is a principle in software development called _the principle of lead privilege_ which is to say default to private data. Only expose what you need to expose. If you make something public, you are reducing your chance at being able to refactor, as if you refactor something that's public you're potentially breaking someone elses code.

## IIFE Pattern

```js
var teacher = "Kyle";
( function anotherTeacher() {
    var teacher = "Suzy";
    console.log(teacher);       // Suzy
})();
console.log(teacher);          // Kyle
```

^ this creates a scope then immediately invokes the function and data within.
This is just invoked and we are done, hence "immediately invoked function expression".

## Block Scoping

## Choosing let or var

## Explicit let Block

## const

## Hoisting

## Hoisting Example

## let Doesn't Hoist
