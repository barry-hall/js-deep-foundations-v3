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
var teacher = "Kyle";

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

// this could also be written as, which is an anonymous IIFE
(function (teacher) {
    console.log(teacher);       // Suzy
})("Suzy");
```

^ this creates a scope then immediately invokes the function and data within.
This is just invoked and we are done, hence "immediately invoked function expression".

## Block Scoping

Block scoping is a lot better than an IIFE.

```js
var teacher = "Kyle";
{
    let teacher = "Suzy";
    console.log(teacher);   // Suzy
}

console.log(teacher);       // Kyle
```

Block are a bit easier and lighter weight to put into place. They aren't expressions, so you can't use them as such.

`let` is a good use of creating a block scoped variable that you have been creating stylisticly (as in using { } to create your scope).

## Choosing let or var

In the following code;

```js
function repeat(fn,n) {
    var result;

    for(let i = 0; i < n; i++) {
        result = fn ( result, i );
    }

    return result
}
```

You could make both variables (`i` & `result`) a `let`. However, if you have a variable that belongs to the entire scope of the function, the correct semantic way to signal that to your reader is not to use a `let` but to use a `var` because that's the thing it's always done.

If you replaced the `var` with a `let` in this example, although it would functionally still work, it would remove a small amount of important semantic information. For example the reader might not know your _intent_. Is your intent for me to use it everywhere? or only at the top of the function?

Lets are supposed to signal a localised use of a variable, ideally a couple of lines. If your intent is to use the variable across the whole function, the `let` will work, but it's not the right tool.

`var` is a more appropriate tool to signal that you have a variable that should be used across the function.

Use `let` it is fantastic and the correct way for block scope. But don't go looking to make things `let` that _should_ be `var`.

```js
function lookupRecord(searchTerm) {
    try {
        var id = getRecord (searchTerm);
    }
    catch(err) {
        var id = -1;
    }

    return id;
}
```

Weahter you intend it or not, using `let` attaches a variable to that scope. So if you were to do a global search and replace for `var` to `let` then the above code would **break**. The reson for this is that there wouldn't be a `id` variable before the return. `id` would exist within the scope of the `try` and the `catch` but not withing `lookupRecord`.

`var` hoists to the function scope. So in the above example `id` exists because it is scoped to `lookupRecord`.

You can also use `var` more than once in a scope. In the above example you are saying to the reader: _"Regardless of what path this takes, there will be a variable called `id`"_.

With this information, it should be clear that both `var` and `let` can co-exist and should be used appropriately.

## Explicit let Block

If you have a variable that only needs to exist for a few lines, make a block for it.

!["explicit let block"](/img/explicit-let-block.png)

This is just a semantic style that potentially helps the reader reason about your code. It means they don't have to go looking around for `prefix` and `rest`. This is also why the `let` keyword is on the same line, it makes this more obvious.

## const

When we think of `const` we think of _a things that doesn't change_. But really it means _a variable that can't be reassigned_.

```js
var teacher = "Suzy";
teacher = "Kyle";       // OK

const myTeacher = teacher;
myTeacher = "Suzy";     // TypeError

const teachers = ["Sid", "Lem"];
teachers[1] = "Carl";   // Allowed!
```

There is a baggage that comes with const that you need to be aware of.

What the `const` is saying from a semantic perspective is: _For the rest of the block I promise it's not going to get reassigned._

A good rule of thumb is only use them on strings, booleans or numbers as these are primitive types.

Constants are supposed to give semantic meaning as placeholders.

**Advice:**

* default to use `var`
* use `let` where it is helpful
* use `const` sparingly only with immutable primitive values.

## Hoisting

**N.B** _This probably needs a bit more explanation but I understand hoisting in general. It is Kyles definition I need to better define._

The JS engine essentially makes two passes over the code. The first pass scans all the variables and declarations and the second one executes them. The first pass is to do a form of "parsin" for the executing engine.

Only declarations are hoisted. Not assignment.

Variables and function definitions are hoisted to the top of their executing scope.

Both `let` and `const` will hoist, it's just that they don't get initialized.
