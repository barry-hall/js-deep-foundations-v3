# Equality

## Double & Triple Equals

== checks value (loose)

=== check value and type (strict)

This isn't _exactly_ the case.

> If you're trying to understand your code, it's critical you learn to think like JS.

As per the spec, both check the types, just one does something different with that information than the other. The source of truth is always the spec. Triple equals shorts the comparison. If they aren't the same "type" no further checking is performed. Double equals will coerce the value first.

== aloows coercion (types different)

=== disallows coercion (types same)

## Coercive Equality

## Double Equals Algorithm

