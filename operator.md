####JavaScript's && operator is coalescing.

```js
js> 0 && 7
0
js> 1 && 7
7
```

&& does not convert things to Boolean values.

&& only continues if it gets a truthy value, returning the first falsy value, or the last value, meaning:

```js
undefined && true == undefined
true && true      == true
true && false     == false
1 && 2 && 3       == 3
1 && 2 && 0 && 4  == 0
```
So if your condition is falsy, e.g. false or undefined, it will return that exact value. If your condition is truthy, it will return whatever doSomethingAndReturnObj() returns.

falsy values for reference: null, undefined, 0, false, NaN, "". everything else is truthy.

```js
var i = 1, j = ++i; // i and j are both 2
var i = 1, j = i++; // i is 2, j is 1
```
```js
var A = 1;
var C = A;
console.log(C); // 1
A++;
console.log(C); // 1
```
But when A is an array we have a different sitiuation. Not only will C change, but it changes before we even touch A

```js
var A = [2, 1];
var C = A;
console.log(C); // [1, 2]
A.sort();
console.log(C); // [1, 2]
```
Arrays are objects. Variables refer to objects. Thus an assignment in the second case copied the reference to the array from "A" into "C". After that, both variables refer to the same single object (the array).

Primitive values like numbers are completely copied from one variable to another in simple assignments like yours. The A++; statement assigns a new value to "A".

The `delete` operator removes a property from an object.

Here are some example uses of the delete operator:

```js
var o = {x:1, y:2}; // Define a variable; initialize it to an object
delete o.x; // Delete one of the object properties; returns true
typeof o.x; // Property does not exist; returns "undefined"
delete o.x; // Delete a nonexistent property; returns true
delete o; // Can't delete a declared variable; returns false.
// Would raise an exception in strict mode.
delete 1; // Argument is not an lvalue: returns true
this.x = 1; // Define a property of the a global object without var
delete x; // Try to delete it: returns true in non-strict mode
```
`delete` doesn't actually destroy the property's value, just the property itself. For example:

```js
var multiverse = {
    earth1: "Silver Age",
    earth2: "Golden Age"
};
var earth3 = "The Crime Syndicate";
multiverse.earth3 = earth3;

delete multiverse.earth3;

console.log(earth3); //The Crime Syndicate
```
