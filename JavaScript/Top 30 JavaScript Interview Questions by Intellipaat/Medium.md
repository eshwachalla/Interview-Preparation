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

A higher-order function in JavaScript is a function that either takes other functions as arguments or returns a function as its result.

```js
function greet(name, greetingFunction) {
  return greetingFunction(name);
}

function sayHello(name) {
  return `Hello, ${name}!`;
}

function sayGoodbye(name) {
  return `Goodbye, ${name}!`;
}

console.log(greet("Alice", sayHello)); // Output: Hello, Alice!
console.log(greet("Bob", sayGoodbye)); // Output: Goodbye, Bob!
```

**Explanation** :

- `greet` is a higher-order function because it takes a function (`greetingFunction`) as an argument.
- `sayHello` and `sayGoodbye` are regular functions that are passed as arguments to `greet`.

## 4. What is an IIFE (Immediately Invoked Function Expression)?

IIFE is a function that runs immediately after it's defined.

```js
(function () {
  console.log("This runs immediately");
})();

Using Parameters:

(function (name) {
  console.log(`Hello, ${name}`);
})("Alice");
```

## 5. Explain closures in JavaScript.

A `closure` is the combination of a function bundled together (enclosed) with references to its surrounding state (the `lexical environment`). In other words, a closure gives a function access to its outer scope. In JavaScript, closures are created every time a function is created, at function creation time.

```js
function outer() {
  var name = "closures"; // name is a local variable created by outer
  function inner() {
    // inner() is the inner function, that forms a closure
    console.log(name); // use variable declared in the parent function
  }
  inner();
}
outer();
```

```js
function outer() {
  let counter = 0;
  return function inner() {
    counter++;
    console.log(counter);
  };
}

const increment = outer();
increment(); // 1
increment(); // 2
```

- `inner` still has access to `counter` even though `outer` has completed.

## 6. How do setTimeout and setInterval work?

- `setTimeout(fn, delay)`: Executes a function `once after a delay` (in milliseconds)
- `setInterval(fn, delay)`: Executes a function `repeatedly every delay milliseconds`

```js
setTimeout(() => {
  console.log("Runs after 2 seconds");
}, 2000);

let count = 0;
const intervalId = setInterval(() => {
  console.log("Repeats every second");
  count++;
  if (count === 3) clearInterval(intervalId); // Stops after 3 runs
}, 1000);
```

## 7. Describe promises in JavaScript.

- A **Promise** in JavaScript is an object that represents the eventual **completion (or failure)** of an asynchronous operation, and its resulting value.
- A Promise is **used to handle asynchronous operations.**
- Instead of using nested callbacks (callback hell), Promises allow you to **write cleaner and more maintainable asynchronous code**.

**States Of Promises**
- A Promise has **three states**:
  1. Pending : The initial state, where operation is still ongoing.
  2. Fulfilled : The operation was successful, and the promise has a result.
  3. Rejected : The operation failed, and the promise has a reason ( error ).

**Creating a Promise**
```js
const myPromise = new Promise((resolve, reject) => {
  // asynchronous operation
  setTimeout(() => {
    const success = true;
    if (success) {
      resolve("Data fetched successfully!");
    } else {
      reject("Error while fetching data");
    }
  }, 2000);
});

// resolve(value) — called when the operation succeeds.
// reject(error) — called when the operation fails.
```

**Consuming a Promise**
- Consuming a promise involves handling its eventual result, whether it resolves successfully or rejects with an error. JavaScript provides the then, catch, and finally methods to manage promises.
```js
function fetchData() {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      const success = true;
      if (success) {
        resolve("Data fetched successfully!");
      } else {
        reject("Failed to fetch data.");
      }
    }, 1000);
  });
}

fetchData()
  .then(data => {
    console.log("Success:", data);
  })
  .catch(error => {
    console.error("Error:", error);
  })
  .finally(() => {
    console.log("Operation complete.");
  });
```

**Explanation**
- **.then()** : This method is used to handle the resolved value of a promise. It takes up to two arguments:
  - **onFulfilled**: A function to be executed when the promise is resolved successfully. It receives the resolved value as an argument.
  - **onRejected**: An optional function to be executed when the promise is rejected. It receives the rejection reason as an argument.
- **.catch()** : This method is used to handle rejections specifically. It takes one argument:
  - **onRejected**: A function to be executed when the promise is rejected. It receives the rejection reason as an argument.
- **.finally()** : This method is used to execute code regardless of whether the promise is resolved or rejected. It takes one argument: 
  - **onFinally**: A function to be executed after the promise is settled (either resolved or rejected). It does not receive any arguments.

**Why use promises?**
- Better **readability** than nested callbacks.
- Easier to chain multiple async tasks using **.then()**.
- Built-in error handling using **.catch()**.

**Chaining Promises**

```js
fetchUser()
  .then((user) => fetchPosts(user.id))
  .then((posts) => displayPosts(posts))
  .catch((error) => console.error(error));

// Each .then() returns a new promise, allowing a smooth flow of asynchronous operations.
```

## 8. Use of async and await in JavaScript.

## 9. Difference between call, apply, and bind.

## 10. What is event delegation?
