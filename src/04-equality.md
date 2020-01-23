# Equality

## Double & Triple Equals

== checks value (loose)

=== check value and type (strict)

This isn't _exactly_ the case.

> If you're trying to understand your code, it's critical you learn to think like JS.

As per the spec, both check the types, just one does something different with that information than the other. The source of truth is always the spec. Triple equals shorts the comparison. If they aren't the same "type" no further checking is performed. Double equals will coerce the value first.

== allows coercion (types different)

=== disallows coercion (types same)

## Coercive Equality

Are you gaining anything readability wise by being explicit?

Coercive Equality: null == undefined

Linters are an opinion on weather your code is structured a certain way. It does not check if your code is correct.

If a tool forces you to do something (i.e. it can't be configured) then that tool isn't helping you.

## Double Equals Algorithm

Double equals favours calling .toNumber on y where x == y.

Coercive Equalty: prefers numberic comparison.

Double equals only compares primitives. If you compare something that _isn't_ a primitive, it will call ToPrimitive(x) == y.

## Double Equals Walkthough

Take this example;

```js
var workshop1Count = 42;
var workshop2Count =  [42];

if(workshop1Count == workshop2Count) {
    // Yep (hmm...)
    // first, it tries to compare workshop1Count and workshop2Count
    // if(42 == "42") is invoked as it calls ToPrimitive on the array, which is a string
    // ^ this is only _accidentally_ working because there is one value in the array
    // if(42 === 42) now we have a number and a string, so favoring numeric, the algorithm coerces the string "42" to a number.
}

```

## Double Equals Summary

## Double Equals Corner Cases

## Corner Cases: Booleans

## Corner Cases: Summary

## The Case for Double Equals

