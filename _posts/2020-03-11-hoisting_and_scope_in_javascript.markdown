---
layout: post
title:      "Hoisting & Scope in Javascript"
date:       2020-03-11 22:17:23 +0000
permalink:  hoisting_and_scope_in_javascript
---


## Background

I've had trouble tackling the concepts of scope & hoisitng in Javascript and sought to create a single testbed script I can use as a reference moving forward.  Here is that testscript:

```javascript
a = 1
var b = 2
let c = 3
const d = 4

if (true){
  w = 5
  var x = 6
  let y = 7
  const z = 8
}

function myFunc1(variable){
  console.log(variable)
}

if (true){
  w = 9
  var x = 10
  let y = 11
  const z = 12
}

a = 14
var b = 15

// let c = 16 // => SyntaxError: Identifier 'c' has already been declared
// const d = 17 // => SyntaxError: Identifier 'd' has already been declared

myFunc1(a) // => 1
myFunc1(b) // => 2
myFunc1(c) // => 3
myFunc1(d) // => 4
myFunc1(w) // => 9
myFunc1(x) // => 10

// myFunc1(y) // => ReferenceError: y is not defined
// myFunc1(z) // => ReferenceError: z is not defined
// console.log(y) // => ReferenceError: y is not defined
// console.log(z) // => ReferenceError: z is not defined

function myFunc2(variable){
  variable = "some new value shadowing the previously defined value"
  console.log(variable)
}

myFunc2(a) // => "some new value shadowing the previously defined value"
myFunc2(b) // => "some new value shadowing the previously defined value"
myFunc2(c) // => "some new value shadowing the previously defined value"
myFunc2(d) // => "some new value shadowing the previously defined value"
myFunc2(w) // => "some new value shadowing the previously defined value"
myFunc2(x) // => "some new value shadowing the previously defined value"

// myFunc2(y) // => ReferenceError: y is not defined
// myFunc2(z) // => ReferenceError: z is not defined

console.log(a) // => 14
console.log(b) // => 15

function myFunc3 () {
  // var myHoistedVariable has been hoised to this position by the engine...
  // but the corresponding identifier "Hello!" has not, and so nothing gets printed.
  console.log(myHoistedVariable);
  // if this variable is declared with let, const, or no prefix at all...
  // you will get: "ReferenceError: myHoistedVariable is not defined"
  var myHoistedVariable = 'Hello!';
}

myFunc3();
```
Now there's a lot going on up there, so here is the same script annotated graphically:

<a href="https://imgur.com/r74HkiE"><img src="https://i.imgur.com/r74HkiE.jpg" title="source: imgur.com" /></a>
You can copy & paste the script into your environment or play around with it in this repl space [here](https://repl.it/@Richard_Burd/Hoisting-and-Scope-Testbed).  &nbsp;
## Source
My main source of input was **Section 3** of ***You Don't Know JS*** by Kyle Simpson available [here](https://rileygelwicks.gitbooks.io/you-dont-know-js/content/scope%20&%20closures/index.html). &nbsp;In [Chapter 1](https://rileygelwicks.gitbooks.io/you-dont-know-js/content/scope%20&%20closures/ch1.html) of that section he lays out an abstraction on a conversation between the Javascript (compiler) engine and the scope(s) involved in the code being read. &nbsp; This helps the reader to understand a little bit of *why* Javascript acts thew way it does.&nbsp;  [Chapter 2](https://rileygelwicks.gitbooks.io/you-dont-know-js/content/scope%20&%20closures/ch2.html) discusses the phenomenon of ***shadowing*** that occurs in my script above inside the ```myFunc3()``` function.&nbsp;  [Chapter 4](https://rileygelwicks.gitbooks.io/you-dont-know-js/content/scope%20&%20closures/ch4.html) has an interesting discussion relevant to that same function which explains why it is exactly...that an assignment will be "...left in place..." and result in an *undefined* output as shown on the last line of my enclosed testbed script.  The other sections were interesting albeit a bit more detailed that what I'm looking for right now.
