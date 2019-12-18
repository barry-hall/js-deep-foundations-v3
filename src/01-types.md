# Types

* Primitive Types
* Abstract Types
* Coercion
* Equality
* TypeScript, Flow, etc

> "In JavaScript, everything is an object."

The reason this is false, is because most of the values in JS can behave like objects, but that does not make them an object. An example of this is "false", which is not an object.

The actual types according to the specification are: _Undefined; Null; Boolean; String; Symbol; Number_ and _Object_.

## Primitive Types

* undefined
* string
* number
* boolean
* object
* symbol

Other things that maybe behave like types.

* undeclared?
* null?
* function?
* array?
* bigint?

These aren't exactly a type but they have behaviour. Does this make them a type? Think of them as "sort of a type", a sub type of the object type i.e. not a "top level" type.

Things can get messy:
![types-objects.png](/img/types-objects.png)

Many of these may have object like behaviours that you can opt into, but they aren't objects.

> In JavaScript, variables don't have types, values do.

## typeof Operator

`typeof` is a way of asking what is the "type" of a value.

```js
var v;
typeof v;       // "undefined"
v = "1";
typeof v;       // "string"
v = 2;
typeof v;       // "number"
v = true;
typeof v;       // "boolean"
v = {};
typeof v;       // "object"
v = Symbol();
typeof v;       // "symbol"
```

`Undefined` essentially means "currently doesn't have a value".

```js
typeof doesntExist;     // "undefined"

var v = null;
typeof v;               // "object"     OOPS!

v = function() {};
typeof v;               // "function" hmmm? (this is not an official "type")

v = [1,2,3]
typeof v;               // "object" hmmm?
```

The reason that null is typeof object is because historically if you wanted to unset a value you would set it to `undefined` and if you wanted to unset an object, you'd set it to `null`. This is actually a bug with JS! It should return "null".

The above examples are some interesting historical things with JavaScript that cannot be fixed, as if we did we'd break a lot of code.

## BigInt

```js
// coming soon!
var v = 42n;    // or: BigInt(42)
typeof v;       //BigInt
```

 BigInt can go infinitely large upto the memory space of the system. It's handy that typeof can determine between the two so we know if we are dealing with a number of a bigint.

## Kinds of Emptiness

**undefined vs undeclared**. These kind of seem to mean the same thing, but they are entirely different.

* _undefined_ means it's definately a variable and at the moment it has no value.
* _undeclared_ means it's never been created in any scope.

typeof operator is the only operator that is able to reference a thing that doesn't exist and not throw an error.

* _uninitialized_—introduced in ES6—is known as the TDZ _(temporal dead zone)_. This means that certain variables (like block scopes) don't get initialized. It never gets set to "undefined", when it is unitialized it is off limits, you're not allowed to touch it in anyway shape or form or you'll get an error, which is the TDZ.

## NaN & isNaN

**Special values**, such as `NaN` and `isNaN`.

NaN doesn't mean not a number. It's a sentinal value that means an "invalid number".

```js
var myAge = Number("0o46");     // 38
var myNextAge = Number("39");   // 39
var myCatsAge = Number("n/a");  // NaN
myAge - "my son's age";         // NaN

myCatsAge === myCatsAge;        // false OOPS!

isNaN(myAge);                   // false
isNaN(myCatsAge);               // true
isNaN("my son's age");          // true OOPS!

Number.isNaN(myCatsAge);        // true
Number.isNaN("my son's age");   // false
```

The reason why NaN doesn't absolutely equal NaN is because the IEEE stated that NaN's aren't equal to one another. An invalid thing cannot be "absolutely" equal to something else which is invalid.

NaN is the only value in JS that doesn't not have the "identity property", therefore it cannot be equal to itself.

The reason `isNaN("my son's age")` returns true is because `isNaN` will coerce the value first before making a comparison. So the coerced value of "my sons age" to a number is `NaN`.

Remember that **NaN: Invalid Number**. Is _is_ a number. It's just not a valid one.

## Negative Zero
