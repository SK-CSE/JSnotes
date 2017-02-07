
## Built-in Types

JavaScript defines seven built-in types:

* `null`
* `undefined`
* `boolean`
* `number`
* `string`
* `object`
* `symbol` -- added in ES6!

**Note:** All of these types except `object` are called "primitives".

```js
typeof undefined     === "undefined"; // true
typeof true          === "boolean";   // true
typeof 42            === "number";    // true
typeof "42"          === "string";    // true
typeof { life: 42 }  === "object";    // true

// added in ES6!
typeof Symbol()      === "symbol";    // true
```
```js
typeof function a(){ /* .. */ } === "function"; // true
typeof [1,2,3] === "object"; // true
```
```js
typeof null === "object"; // true
var a = null;
(!a && typeof a === "object"); // true
```

The typeof operator always returns a string. So:

```js
typeof typeof 42; // "string"
```
The first typeof 42 returns "number", and typeof "number" is "string".

### `undefined` vs "undeclared"

Variables that have no value *currently*, actually have the `undefined` value. Calling `typeof` against such variables will return `"undefined"`:

```js
var a;

typeof a; // "undefined"

var b = 42;
var c;

// later
b = c;

typeof b; // "undefined"
typeof c; // "undefined"
```
Consider:

```js
var a;

a; // undefined
b; // ReferenceError: b is not defined

typeof a; // "undefined"
typeof b; // "undefined"
```

The `typeof` operator returns `"undefined"` even for "undeclared" (or "not defined") variables. Notice that there was no error thrown when we executed `typeof b`, even though `b` is an undeclared variable. This is a special safety guard in the behavior of `typeof`.
