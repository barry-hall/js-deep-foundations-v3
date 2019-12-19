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

Here us a table of using the toNumber() operator on various types.

| type      | result    |
|---        | ---       |
| ""        | 0         |
| "0"       | 0         |
| "-0"      | -0        |
| " 009 "   | 9         |
| "3.14159" | 3.14159   |
| "0."      | 0         |
| ".0"      | 0         |
| "."       | NaN       |
| "0xaf"    | 175       |

Numberfication of falses / trues etc.

| type      | result    |
| ---       | ---       |
| false     | 0         |
| true      | 1         |
| null      | 0         |
| undefined | NaN       |

When we use toNumber() on a non primitive (object) it invokes the toPrimitive() operator with the number hint, which in turn calls valueOf() and toString().

## toBoolean

Anytime you have any value that isn't a boolean, and it is used in a place that needs a boolean, this happens...

Falsy means value that will return false when coerced to a boolean.

| Falsey    | Truthy            |
| ---       | ---               |
| ""        | "foo"             |
| 0, -0     | 23                |
| null      | {a:1}             |
| NaN       | [1,3]             |
| false     | true              |
| undefined | function(){..}    |

Note in the above example, if anything is _not_ in the falsy list then it is always considered truty. The items in the Truthy column are just example values.

## Cases of Coercion

We all use coercion all the time. e.g. template strings. Below the number is implicitly getting coerced into a string. This isn't a bad thing...

```js
var numStudents = 16;
console.log(
    `There are ${numStudents} students.`
)
```

If you concatenate a number and a string, the result will always have toString() applied to it.

If you wanted to explitily coerce your value this would be the preferred way...

```js
var numStudents = 16;
console.log(
    `There are ${String(numStudents)} students.`
)
```

To explicitly add a number you'd use something like the following;

```js
function addAStudent(numStudents) {
    return numStudents + 1;
}

addAStudent(
    Number(studentsInputElem.value) // explicitly passing a number...
)
```

You have to be careful with coercion with booleans. In the below example, if `studentsInputElem.value` was a bunch of white space, the if statement would resolve as truthy... although this isn't a string you'd care about, it would be valid for the if!

```js
if(studentsInputElem.value) {
    numStudents =
        Number(stundentsInputElem.value);
}

// ***************************
Boolean("");        // false
Boolean(" \t\n");   // true OOPS!
```

We should be more explicit in our intent. Example;

```js
//this is essentially saying while "truthy"
while(newStudents.length) {
    enrollStudent(newStudents.pop());
}

// the below will protect you from more corner cases, but not all.
// this is far more explicit and much better.
while(newStudents.length > 0) {
    enrollStudent(newStudents.pop());
}
```

Boolean will test for undefined & null (on the falsy list) but where possible treat null and undefined as indistinguishable. Coerceion is helpful for this. "Has this thing been set or not" is a perfectly reasonable implicity boolean coercion.

```js
var workshop = getRegistration(student);

if(workshop) {
    console.log(
        `Welcome ${student.name} to ${workshop.name}.`
    )
}

// **********************
Boolean(undefined)  // false
Boolean(null)       // false
Boolean({})         // true
```

## Boxing

Boxing is a form of implicit coercion. e.g. `studentNameElem.value.*length*`. Here it is saying, "you have this thing that is not an object and you're trying to use it as an object. Me as JavaScript I'm going to be helpful and go ahead and make it into an object for you".

Boxing is also one of the reason why everyone seems to think that everything in JS is an object. Because boxing is taking place.

Weather we call things coercion or conversion, all proigramming language have type converions, because it is absolutely necessary.

## Corner Cases of Coercion

Every language has type conversion corner cases and JS is no exception. Here is a list of interesting ones.

```js
Number( "" );                   // 0    OOPS!
Number( "  \t\n");              // 0    OOPS!
Number( null );                 // 0    OOPS!
Number( undefined );            // NaN
Number( [] );                   // 0    OOPS!
Number( [1,2,3] );              // NaN
Number( [null] );               // 0    OOPS!
Number( [undefined] );          // 0    OOPS!
Number( {} );                   // NaN

String( -0 );                   // "0"  OOPS!
String( null );                 // "null"
String( undefined );            // "undefined"
String( [null] );               // ""   OOPS!
String( [undefined] );          // ""   OOPS!

Boolean( new Boolean(false) );  // true OOPS!
```

**The root of all (coercion) evil...**

```js
studentsInput.value = "";
// ..
Number(students.Input.value):   // 0
studentsInput.value = "  \t\n";
// ..
Number(students.Input.value):   // 0
```
