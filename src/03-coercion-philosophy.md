# Philosophy of Coercion

## Intentional Coercion

Adopt a coding style that makes your types more obvious. Make your types plain. JavaScript's dynamic typing is not a weakness, it's one of its strong qualities.

## Culture of Learning

Be empathatic in code reviews. Don't be a gate keeper. Don't think junior developers "wont get it". Don't care where you are, care what your direction is. You should use tools well and not be "clever". Your code is a form of communication. There is an effective way to communicate that understands and uses the tool well. Don't let someone get to see you use a "trick" that they never see or use again. Take the time to invest in a way that will help them progress. Tricks might make certain people feel good but they are a waste of someone elses time.

Everyone should be able to interoperate on a codebase. A junior will have to learn some stuff, sure. But you should all be effective at some level.

## Implicit Coercion

Implicitness is abstraction. Implicitness is not bad, it's the inaprorpiate use of abstraction. Hide unnecessary details, re-focusing the read and increasing clarity.

Coercion: implicit can be good (sometimes)

```js
var numStudents = 16;
console.log(
    `There are ${String(numStudents)} students.` // if we are dealing with corner cases, this is fine.
)
// "There are 16 students."
var numStudents = 16;
console.log(
    `There are ${numStudents} students.`
)
// "There are 16 students."
```

> Is showing the reader the extra type details helpful or distracting?

Be an engineer, not a code monkey. Think critically and analytically.

## Understanding Features

> "If a feature is sometimes **useful** and sometimes **dangerous** _and if there is a better option_ then always use the better option."—"The Good Parts", Crockford

**Useful**: when the reader is focused on what's important.

**Dangerous**: when the reader can't tell what will happen.

**Better**: when the reader understands the code.

> It is _irresponsible_ to knowingly avoid usage of a feature that can and does _improve code readability_.
