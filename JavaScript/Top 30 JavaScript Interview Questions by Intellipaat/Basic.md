## 1. What is JavaScript and its common uses?

JavaScript is a high-level, interpreted programming language primarily used for adding interactivity and dynamic behavior to websites. It runs in the browser and is a core technology of the web alongside HTML and CSS.

**Common Uses :**

- Creating interactive web pages (forms, sliders, animations)
- DOM manipulation
- Client-side form validation
- Making API calls (AJAX/fetch)
- Game development
- Backend development using Node.js
- Building web apps with frameworks like React, Angular, Vue.js

## 2. What are template literals in JavaScript?

Template literals are strings that allow embedded expressions, multiline strings, and string interpolation.

**Syntax :**

```js
let name = "John";
let greeting = `Hello, ${name}!`; // Interpolation
console.log(greeting); // Output: Hello, John!
```

## 3. What is hoisting? Provide an example?

Hoisting essentially means that JavaScript moves the declarations of variables and functions to the top of their scope, but only the declarations, not the initializations or assignments.
**How it works:**

- **Variable Declarations**: When a variable is declared using `var`, its declaration is hoisted, and the variable is initialized with the value `undefined`.
- **Function Declarations**: Function declarations are also hoisted, meaning you can call a function before it's declared in the code.
- **Function Expressions**: Function expressions (functions assigned to variables) are **not hoisted** in the same way as function declarations.

```js
console.log(myVariable); // Output: undefined (due to hoisting)
var myVariable = "Hello";
console.log(myVariable); // Output: Hello
```

- Important Notes:
  - `let` and `const` declarations are also hoisted, but they are not initialized until their declaration is reached, resulting in a "Temporal Dead Zone" where accessing them before their declaration will result in a ReferenceError.
  - Hoisting can be confusing, but understanding it is crucial for writing more predictable and maintainable JavaScript code.
  - It's a good practice to declare variables and functions at the top of their scope to avoid potential issues related to hoisting.

## 4. Difference between let, var, and const.

- var is a function-scoped whereas let and const is a block-scoped

```js
function testVar() {
  if (true) {
    var a = 10;
  }
  console.log(a); // ✅ 10 (accessible outside block)
}

function testLetConst() {
  if (true) {
    let b = 20;
    const c = 30;
  }
  console.log(b); // ReferenceError: b is not defined
  console.log(c); // ReferenceError: c is not defined
}

testVar();
testLetConst();
```

- var can be hoisted ( Initialized to Undefined ), but let and const are hoisted in temporal dead zone ( TDZ )

```js
console.log(x); // undefined (hoisted)
var x = 5;

console.log(y); // ReferenceError: Cannot access 'y' before initialization
let y = 10;

console.log(z); // ReferenceError: Cannot access 'z' before initialization
const z = 15;
```

- var and let can be reassignable but const cant be re-assigned.

```js
var a = 1;
a = 2; // allowed

let b = 3;
b = 4; // allowed

const c = 5;
c = 6; // TypeError: Assignment to constant variable.
```

- Only var can be redeclarable whereas let and const cant be redeclared

```js
var d = 1;
var d = 2; // allowed

let e = 3;
let e = 4; // SyntaxError: Identifier 'e' has already been declared

const f = 5;
const f = 6; // SyntaxError: Identifier 'f' has already been declared
```

## 5. Data types in JavaScript ?

JavaScript has 8 data types:

- Primitive Types ( Immutable ) : `String`, `Number`, `BigInt`, `Boolean`, `Undefined`, `null`, `Symbol`
- Non-Primitive Types : `Object` ( Array, Functions, Dates )

## 6. What is an array, and how to access its elements?

An array is a special type of object that stores ordered collections of items (elements), accessed by index.

- Indexing starts from 0
- Arrays are mutable

```js
let fruits = ["apple", "banana", "cherry"];
console.log(fruits[0]); // Output: apple
```

## 7. Difference between == and ===.

- `==` also known as `Loose Equality` compares only value ( 5 == "5" -> True )
- `===` also known as `Strict Equality` compares value and type both ( 5 === "5" => False )
- Use Strict Equality (`===`) for safer and predictable comparison.

## 8. Purpose of the isNaN function.

`isNaN(value)` checks whether a value is `NaN` (Not-a-Number) or not. It tries to convert the value to a number first.

```js
console.log(isNaN("hello")); // true
console.log(isNaN(123)); // false
```

For strict checking, use `Number.isNaN()`:

```js
Number.isNaN("hello"); // false
Number.isNaN(NaN); // true
```

## 9. What is `null` vs `undefined`?

`Undefined` is automatically assigned to a variable that is declared but has not been assigned a value, while `null` is assigned manually to indicate the intentional absence of a value

```js
let a;
console.log(a); // undefined

let b = null;
console.log(b); // null
```

## 10. Use of the typeof operator?

`typeof` is used to check the data type of a variable or value.

```js
console.log(typeof 42); // "number"
console.log(typeof "hello"); // "string"
console.log(typeof true); // "boolean"
console.log(typeof undefined); // "undefined"
console.log(typeof null); // "object" (known JS quirk)
```
