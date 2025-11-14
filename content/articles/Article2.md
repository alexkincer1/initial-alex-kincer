---
title: "Chapter Five: Flattening a Loop"
description: ""
omit_header_text: true
featured_image:
summary: "Flattening arrays into a single array while keeping all elements present."
type: page
weight: 3
---


This article comes from information gathered in reading [Chapter Five in Eloquent JavaScript](https://eloquentjavascript.net/05_higher_order.html). Once the lesson was learned, CSC 324 provided [this Homework Assignment](https://homerhanumat.github.io/csc324resources/exercises/eloquent-ch05.html). This article will discuss and break down Exercise One, Flattening.

## The Assignment Details

Use the reduce method in combination with the concat method to “flatten” an array of arrays into a single array that has all the elements of the original arrays.

<blockquote>
Though I recieved this answer from classmate Jose's screenshare that prompted in-depth discussion for the CSC 324 class on Septmeber 25, 2025, I will use this article to explain line by line what the code is doing and why each function was chosen.
</blockquote>


## Solution

#### Creating the Array

This following line of code creates a variable called `arrays` that then lists the values assigned to it. 
```js
let arrays = [[1, 2, 3], [4, 5], [6]];
```
The key component of this line is the term `let` that allows the declared variable to be able to be reassigned later. 

The way these values are listed is referred to as a nested array which hold three seperate arrays inside the one larger array.

```js
let flattened = arrays.reduce((acc, curr) => acc.concat(curr), []);
```
The above line begins the flattening process by using the `.reduce()` function to take one element from the array at a time and slowly build up a single value. Following this command, `acc` and `curr` are then used to move on. `acc` starts as [] and grows as numbers are added to ultimately become the flattened array. `curr` is used for the nested array to be kept as, in this case, three values for three steps. Finally, for this step, `.concat()` merges two arrays at a time to produce a flattened single array.


The following line then prints the value of the flattened variable to the console. When this line is run, the array will print out into the console.

```js
console.log(flattened);
```
The following line prints a similar string to the console but with an extra.

```js
console.log("\n Or ");
```
`\n` is a new line character that tells the console to move to the next line before printing the results. `Or` is the text that will be printed on the following line.

```js
let arrays2 = [[1, 2, 3], [4, 5], [6]];
```
The line above creates a new variable called `arrays2` and assigns a three array nested array to it. Similar to earlier, this preps the arrays to be flattened.

```js
let flattened2 = arrays2.reduce((acc, curr) => {
    return acc.concat(curr);
 }, []);
```
The code chunk above is the exact same as it was for `flattened` and `arrays` earlier so the arrays can be manipulated into being flattened. 
```js
 console.log(flattened2);
```
Also like before, `console.log` is used to print the newly flattened set of arrays into one array.

Finally, the following chunk is the same as both the original and test 2 to create, nest, and flatten an array using the same kind of commands but different numbers, etc. for the manipulation.

```js
let flattened3 = arrays3.reduce((acc, curr) => {
    return acc.concat(curr);
}, []);
console.log(flattened3);
```

We are done!

## Full Code

Here is a compelete solution ot the problem for readers for view below:

```js
let arrays = [[1, 2, 3], [4, 5], [6]];

let flattened = arrays.reduce((acc, curr) => acc.concat(curr), []);

console.log(flattened);

console.log("\n Or ");

let arrays2 = [[1, 2, 3], [4, 5], [6]];

let flattened2 = arrays2.reduce((acc, curr) => {
    return acc.concat(curr);
 }, []);

 console.log(flattened2);

let arrays3 = [3, [1, 2], [4, 5]];
let flattened3 = arrays3.reduce((acc, curr) => {
    return acc.concat(curr);
}, []);
console.log(flattened3);
```
