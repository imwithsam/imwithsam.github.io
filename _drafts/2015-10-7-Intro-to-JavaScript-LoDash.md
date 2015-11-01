---
layout: post
title: Intro to JavaScript - Lo-Dash
---

This post covers the [nodeschool.io](http://nodeschool.io/) tutorial
[Lololodash](https://github.com/mdunisch/lololodash). Read my first post on
[JavaScripting](Intro-to-JavaScript-JavaScripting) if you haven't already.

## Lololodash - Learn Lo-Dash
[Lo-Dash](https://lodash.com/) is a fork of
[underscore.js](http://underscorejs.org/), a JavaScript utility library
providing many useful helper functions. Without going into all the history and
politics, the general consensus is that Lo-Dash is an improvement over
Underscore. There are talks, however, of the two libraries merging.

### Naming Files
The tutorial doesn't explicitly state this, but I recommend saving your scripts
based on the function being learned for each exercise. e.g. `where.js`,
`sort-by.js`, etc.

### Module Not Found
One of the most helpful things I can tell you about this tutorial is that if you
receive a vague `fail.module_not_found` error when running or verifying your
code, you most likely have a syntax error somewhere. Check for matching
parentheses and curly braces. If all else fails, you can always open an issue on
the [NodeSchool discussion repo](https://github.com/nodeschool/discussions).

### Strict Mode
After your code is verified with a correct answer, you will be given the
tutorial's official solution. One thing to note is the use of `'use strict';` at
the beginning of each script. This line is optional, but generally considered a
good JavaScript coding practice. It was introduced with ECMAScript 5. [John
Resig](http://ejohn.org/), creator of the famous [jQuery](https://jquery.com/)
JavaScript library, has a good post about [ECMAScript 5 Strict
Mode](http://ejohn.org/blog/ecmascript-5-strict-mode-json-and-more/).

The first four exercises are pretty straight forward. When you get to the
**REVISING STRINGS** exercise, note that the `replace()` function is
non-destructive. In other words, it does not mutate the `pizza` variable. When
you call `pizza.replace('alright', 'wonderful');` the pizza variable is not
changed. So if you were to do a `console.log(pizza);` you would still get "pizza
is alright." In order to change the pizza variable, you must assign it by
calling `pizza = pizza.replace('alright', 'wonderful');` Now, when you call
`console.log(pizza);` it will output "pizza is wonderful."

The same is true for the `Math.round()` function in the **ROUNDING NUMBERS**
exercise. You must assign the `roundUp` variable back to itself to change its
value. i.e. `roundUp = Math.round(roundUp);` Note the
[camelCase](https://en.wikipedia.org/wiki/CamelCase) naming convention used in
JavaScript. Also, I recommend using single-quotes in JavaScript as it tends to
be the more common convention. The most important thing is to be consistent with
whatever conventions you and anyone you're working with choose to use.

In the **FOR LOOPS** exercise, they give you `total += i;` to add the variable
`i` to the `total` variable. This is just a shorter way of writing `total =
total + i;`.

Things really start to get interesting in the **ARRAY FILTERING** exercise. In
the example, they pass an anonymous function to the `filter()` method. An
anonymous function simply means a function without a name. In the challenge,
they have you pass a named function (named "evenNumbers") to the `filter()`
method. The main difference between an anonymous function and a named one is
that you can define a named function elsewhere in your code and reference it
like you do with variables. There's a lot going on in this exercise so if you
feel a bit lost don't worry. It will all start to make more sense with a little
practice. A great JavaScript reference is the [Mozilla Developer Network
(MDN)](https://developer.mozilla.org/). Here you can learn more about how the
[filter
function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)
and other functions (also referred to as methods) work. SPOILER ALERT: Since
this exercise can be a little tricky, I have posted the answer below. Try to
figure it out on your own first, and don't copy-and-paste.

```javascript
var numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
var filtered = numbers.filter(evenNumbers);
console.log(filtered);

function evenNumbers(number) {
  return number % 2 === 0;
}
```

Note that the `evenNumbers()` function [does not need to be defined before it is
called](https://javascriptweblog.wordpress.com/2010/07/06/function-declarations-vs-function-expressions/).
The `filter()` function will pass each element in the `numbers` array to the
`evenNumbers()` function. The `%` operator means divide by and return the
remainder. In this case, we are dividing by 2 and checking for a remainder of 0
to determine if the number is even. JavaScript requires you to use the `return`
statement if you wish to return a value from a function. In this case, we are
returning a boolean (`true` or `false`) to the `filter()` function. You may be
wondering why they use a triple-equals instead of a double-equals for a
comparison operator.  You will usually use a triple-equals comparison operator
in JavaScript. MDN has a good explanation of [equality comparisons and
sameness](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Equality_comparisons_and_sameness)
in JavaScript. Another great resource is the book ["JavaScript: The Good
Parts"](http://www.amazon.com/JavaScript-Good-Parts-ebook/dp/B0026OR2ZY/) by
[Douglas Crockford](http://javascript.crockford.com/).

There are a couple of ways you could solve the **LOOPING THROUGH ARRAYS**
exercise. You could write your for loop as `for (var i = 0; i < 3; i++)`. It
would be better, however, to make the for loop more versatile by writing it as
`for (var i = 0; i < pets.length; i++)`. This way, it will still work if you add
or remove elements to or from the array.

Lastly, the **SCOPE** exercise is another leap in interestingness like the ARRAY
FILTERING exercise. And like that exercise, don't worry if you don't understand
everything right away. I recommend experimenting with this one in the console or
JS Bin. Try figuring out what each variable's value will be in each function
first. Then, `console.log()` the values in each function to check yourself.
Don't worry too much about the [Immediately Invoked Function
Expression](http://benalman.com/news/2010/11/immediately-invoked-function-expression/).
All that's doing is surrounding each function with parentheses so they'll be
executed without having to explicitly call them.
