---
layout: post
title: Intro to JavaScript - JavaScripting
---

If you're just starting out learning JavaScript,
[nodeschool.io](http://nodeschool.io/) is a good place to begin. There are
plenty of articles out there that show you how to get everything set up so I
won't go into that here. Instead, I will cover some interesting points and fill
in the gaps from the
[JavaScripting](https://github.com/sethvincent/javascripting) tutorial.

## JavaScripting
One of the most useful tools for writing and debugging JavaScript is the
JavaScript console in your web browser. Every major browser has a JavaScript
console built in. In Chrome, you can access it by navigating to *View ->
Developer -> JavaScript Console* in the browser menu bar. This will bring up a
split pane at the bottom of your browser containing the browser's Developer
Tools with the Console tab selected. In this console, you can type or
copy-and-paste the JavaScript you write in your NodeSchool files. This will
allow you to see the output of your JavaScript in addition to running
`javascripting verify` on your file and seeing the success message. If you're
feeling adventurous, you can also use a site like [JS
Bin](http://jsbin.com/?js,console,output) to help you test out your JavaScript.

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
executed without having to call them explicitly.
