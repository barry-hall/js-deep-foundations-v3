# Coercion

## Abstract Operations

These are the fundamental building blocks of how we deal with type conversion. Coercion is type conversion. They are interchangable.

If you are going to use something that isn't a primitive in some place that needs primitives e.g. in a math or concatenation, in your mind you should be aware js is going to invoke the valueOf and toString methods in order to coerce the value.

## toString

Conversion table of results from calling toString on various types.

| type      | toString      |
|---        |---            |
| null      | "null"        |
| undefined | "undefined    |
| true      | "true"        |
| false     | "false"       |
| 3.14159   | "3.14159"     |
| 0         | "0"           |
| -0        | "0"           |

**ToString(object) : _is going to invoke_ ToPrimitive(string) which is going to call first, toString() then valueOf()**.

Arrays:

| input             | result    |
|---                | ---       |
| []                | ""        |
| [null, undefined] | ","       |
| [[[],[],[]]]      | ",,,"     |
| [,,,,]            | ",,,"     |

Objects:

| input                     | result                |
|---                        | ---                   |
| {}                        | "[object, Object]"    |
| {a:2}                     | "[object, Object]"    |
| { toString( return "X";}} | "X"                   |

Notice how they left the square brackets off of arrays, but not off objects!

You can override the toString method to be more helpful. e.g. you could json.Stringify the object to help you out in the dev console.

## toNumber


## toBoolean

## Cases of Coercion

## Boxing

## Corner Cases of Coercion