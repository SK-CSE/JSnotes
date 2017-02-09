### String
```js
var a = new String( "abc" );

typeof a; // "object" ... not "String"

a instanceof String; // true

Object.prototype.toString.call( a ); // "[object String]"
```
The point is, `new String("abc")` creates a string wrapper object around `"abc"`, not just the primitive `"abc"` value itself.

```js
var a = new Boolean( false );

if (a) {
    console.log( "Oops" ); // Oops
}
console.log(a) // [Boolean: false]
```
The problem is that you've created an object wrapper around the false value, but objects themselves are "truthy"
```js
var a = false;

if (a) {
    console.log( "Oops" ); // never runs
}
console.log(a); // false
```
```js
var a = "abc";
var b = new String( a );
var c = Object( a );

console.log(typeof a); // "string"
console.log(typeof b); // "object"
console.log(typeof c); // "object"

console.log(a instanceof String); // false
console.log(b instanceof String); // true
console.log(c instanceof String); // true
```
```js
var a = new String( "abc" );
var b = a + ""; // `b` has the unboxed primitive value "abc"

typeof a; // "object"
typeof b; // "string"
```
