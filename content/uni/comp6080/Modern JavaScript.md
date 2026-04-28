---
title: Modern JavaScript
draft: false
tags:
  - webdev
  - computer-science
  - js
---
This week I will be learning [[Modern JavaScript]] as part of my preparation for [[comp6080]]. I'm not new to [[Javascript]], having used it in [[comp1531]] for the [[backend]] project. However, that was last year, and I stuck to fundamental [[loops]], [[functions]] and [[data structures]] like [[hash maps]] and [[arrays]]. I was recommended by [[Gemini]], to look further into [[Modern JavaScript]], with the promise that it would be of great help starting [[comp6080]], so this note will serve as a reference to any concepts I discover within [[Javascript]] that are worth noting.

## [Arrow Functions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions)

This way of writing a function originates from [ES6](https://en.wikipedia.org/wiki/ECMAScript), and it lets use write a function in just one line:

Normal function:
```
function sum(a, b) {
return a + b;
}
```

Arrow function:
```
let sum = (a, b) => a + b;
```
We replace the function keyword (since it's assumed) and we instead assign the function to a keyword. Between the parenthesis are arguments, and anything after the arrow is assumed to be returned.

Why we use this apart from it being more efficient to write is for anonymous functions. If we call a function as a method of an object, in an arrow function, ***this*** points to the object, whereas in a normal function, ***this*** is redefined to the global scope, depending on where the function was called, that's why it is helpful when writing anonymous functions like:

```
printNameArrow() {
	setTimeout(() => {
		console.log('Arrow: ' + this.name)
	}, 100)
```

## [Template Literals](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals)

These are literals that use the backtick. They're useful for [multi-line strings](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals#multi-line_strings) and [string interpolation](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals#string_interpolation).

Examples:
```
`string text`

`string text line 1
 string text line 2`

const expression = 'wow';

`string text ${expression} string text`
```

## [Destructuring](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring)


This syntax allows us to easily unpack items in an array into distinct values.

Examples:
```
let a, b, rest;
[a, b] = [10, 20];

console.log(a);
// Expected output: 10

console.log(b);
// Expected output: 20

[a, b, ...rest] = [10, 20, 30, 40, 50];

console.log(rest);
// Expected output: Array [30, 40, 50]
```

## [Spread](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax)

This syntax allows for elements of a string or array to be assigned to parameters of a function.

Example:
```
function sum(x, y, z) {
  return x + y + z;
}

const numbers = [1, 2, 3];

console.log(sum(...numbers));
// Expected output: 6

console.log(sum.apply(null, numbers));
// Expected output: 6
```

## Promises

## Async/Await
