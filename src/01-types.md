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

## BigInt

## Kinds of Emptiness

## Nan & isNaN

## Negative Zero
