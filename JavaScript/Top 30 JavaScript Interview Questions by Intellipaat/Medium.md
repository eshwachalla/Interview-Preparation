## 1. Purpose of the map method in JavaScript?

The `map()` method is used to iterate over an array and create a new array by applying a function to each element. It does not modify the original array.

```js
const numbers = [1, 2, 3, 4];
const doubled = numbers.map((num) => num * 2);
console.log(doubled); // [2, 4, 6, 8]
```

## 2. Explain event bubbling and event capturing.

**Event Bubbling:**
`Event Bubbling` is a phase of event propagation in the DOM where an event starts at the `target element` and then `bubbles up` (propagates) through its ancestors (parent → grandparent → up to the root of the DOM).

You can use `event.stopPropagation()` to prevent the bubbling.

```html
<div id="parent">
  <button id="child">Click Me</button>
</div>
```

```js
document.getElementById("child").addEventListener("click", () => {
  console.log("Child clicked");
});

document.getElementById("parent").addEventListener("click", () => {
  console.log("Parent clicked");
});
```

```
Output:

Child clicked
Parent clicked
```

If you want to prevent the event from bubbling to parent elements, use `event.stopPropagation()`

```js
document.getElementById("child").addEventListener("click", (e) => {
  e.stopPropagation();
  console.log("Child clicked");
});
```

```
Output:

Child clicked
```

**Event Capturing:**
Event Capturing (also known as trickling phase) is a phase of event propagation in JavaScript where the event starts from the top (root) of the DOM and trickles down to the target element.

```html
<div id="outer">
  <div id="inner">
    <button id="btn">Click Me</button>
  </div>
</div>
```

```js
document.getElementById("outer").addEventListener(
  "click",
  () => {
    console.log("Outer Div - Capturing");
  },
  true
); // 👈 `true` enables capturing

document.getElementById("inner").addEventListener(
  "click",
  () => {
    console.log("Inner Div - Capturing");
  },
  true
);

document.getElementById("btn").addEventListener(
  "click",
  () => {
    console.log("Button - Target");
  },
  true
);
```

```
Output:

Outer Div - Capturing
Inner Div - Capturing
Button - Target
```

- The event starts at the outermost ancestor (`outer`), then goes down to `inner`, and finally reaches the button.
- This is `top-down propagation`.

## 3. What are higher-order functions? Provide an example.


## 4. What is an IIFE (Immediately Invoked Function Expression)?
## 5. Explain closures in JavaScript.
## 6. How do setTimeout and setInterval work?
## 7. Describe promises in JavaScript.
## 8. Use of async and await in JavaScript.
## 9. Difference between call, apply, and bind.
## 10. What is event delegation?
