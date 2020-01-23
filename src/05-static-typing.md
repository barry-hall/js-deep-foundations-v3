# Static Typing

## TypeScript & Flow

type-aware linting...

Benefits:

1. Catch type-related mistakes
2. Communicate type intent
3. Provide IDE feedback

Caveats:

1. Inferencing is best-guess, not a guarantee
2. Annotations are optional
3. Any part of the application that isn't typed introduces uncertainty

## Inferencing

```js
var teacher = "Kyele";
// ..
teacher = { name: "Kyle" };
// Error: can't assign object to string
```

## Custom Types

```js
type student = { name: string };

function getName(studentRec: student) : string {
    return studentRec.name;
}

var firstStudent: student = { name: "Frank" };
var firstStudentName: string = getName(firstStudent);
```

## Validating Operand Types

Undervalued within typescript is it can tell us if certain operations are invalid...

```js
var studentName: string = "Frank";

var studentCount: number = 16 - studentName;
// error: can't subtract string
```

## TypeScript & Flow Summary

[Further reading on typescript & flow](https://github.com/niieani/typescipt-vs-flowtype). A good comparison of similarities and differences.

## Static Typing Pros

* They make the types much more obvious in your code. This is a big improvement over uncertainty
* Familiarity: they look like other language's type systems
* Extremely popular these days
* These aren't going anywhere and any investment into learning will pay off long term

If you are primarily a dotNET developer, it makes a lot of sense to continue using a type system if you need it when it comes to writing some JavaScript.

## Static Typing Cons

* They use "non-JS-standard" syntax (or code comments)
* They require* a build process, which raises the barrier to entry
* Their sophistication can be intimidating to those without prior formal types experience
* They focus more on "static types" (variables, parameters, returns, properties, etc) than _value types_

## Understanding Your Types

JavaScript has a (dynamic) type system, which uses various forms of coercion for value type conversion, including equality comparisons.

However, the prevailing repsonse seems to be: avoid as much of this system as possible, and use `===` to "protect" from needing to worry about types.

Part of the problem with _avoidance_ of whole swaths of JS, like pretending `===` saves you from needing to know types, is that it tends to systemically perpetuate bugs.

You simply cannot write quality JS programs without knowing the types involved in your operations.

Alternately, many choose to adopt a different "static types" system layered on top.

While certainly helpful in some respects, this is "avoidance" of a different sort.

Apparently, JS's type system is inferior so it must be replaced, rahter than learned and leveraged.

Many clam that JS's type system is too difficult for newer devs to learn, and that static types are (somehow) more learnable.

> [@getify](https://twitter.com/getify)—My claim: the better approach is to embrace and learn JS's type system, and to adopt a coding style which makes types as obvious as possible.

By doing so, you will make your code more readable and more robust, for experienced and new developers alike.

As an option to aid in that effort, Getify created Typl, which embraces and unlocks the best parts of JS's types and coercion.
