---
theme: seriph
background: https://raw.githubusercontent.com/mdn/content/main/files/en-us/web/api/document_object_model/dom_tree.png
title: Javascript Promises
class: text-center
transition: slide-left
layout: cover
---

# Javascript Promises, Async/Await

From pending uncertainty to settled certainty: Promises bring order to the wild world of async JavaScript

<div @click="$slidev.nav.next" class="mt-12 py-1" hover:bg="white op-10">
  Press Space for next page <carbon:arrow-right />
</div>

<div class="abs-br m-6 text-xl">
  <button @click="$slidev.nav.openInEditor()" title="Open in Editor" class="slidev-icon-btn">
    <carbon:edit />
  </button>
  <a href="https://github.com/slidevjs/slidev" target="_blank" class="slidev-icon-btn">
    <carbon:logo-github />
  </a>
</div>

---
transition: fade-out
---

# What are Javascript Promises?

A JavaScript Promise is an object that represents the eventual completion (or failure) of an asynchronous operation and its resulting value. It serves as a placeholder for a value that may not be available yet but will be at some point in the future.

A Promise can be in one of three states:

-  **Pending** - The initial state. The asynchronous operation is still in progress and the promise has neither been fulfilled nor rejected
- **Fulfilled (or Resolved)** - The asynchronous operation completed successfully, and the promise now has a resulting value
- **Rejected** - The asynchronous operation failed, and the promise has a reason for the failure (an error).
<br>
<br>



<style>
h1 {
  background-color: #2B90B6;
  background-image: linear-gradient(45deg, #4EC5D4 10%, #146b8c 20%);
  background-size: 100%;
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
</style>

---

The Promise object supports two properties: state and result.

While a Promise object is "pending" (working), the result is undefined.

When a Promise object is "fulfilled", the result is a value.

When a Promise object is "rejected", the result is an error object.


	
| myPromise.state                   | myPromise.result                |
| ------------------------ | -------------------------- |
| "pending"           | undefined           |
| "fulfilled"            | a result value         |
| "rejected"            | an error object         |


---


# JavaScript Promise Object

-A Promise contains both the producing code and calls to the consuming code:

```js
let myPromise = new Promise(function(myResolve, myReject) {
// "Producing Code" (May take some time)

  myResolve(); // when successful
  myReject();  // when error
});

// "Consuming Code" (Must wait for a fulfilled Promise)
myPromise.then(
  function(value) { /* code if successful */ },
  function(error) { /* code if some error */ }
);
```
When the producing code obtains the result, it should call one of the two callbacks:


| When                   | Call                |
| ------------------------ | -------------------------- |
| Success            | myResolve(result value)           |
| Error            | myReject(error object)         |

---

# Promise How To

- Here is how to use a Promise:

```js
myPromise.then(
  function(value) { /* code if successful */ },
  function(error) { /* code if some error */ }
);
```
Promise.then() takes two arguments, a callback for success and another for failure.

Both are optional, so you can add a callback for success or failure only.

---

- Example

```js
function myDisplayer(some) {
  document.getElementById("demo").innerHTML = some;
}

let myPromise = new Promise(function(myResolve, myReject) {
  let x = 0;

// The producing code (this may take some time)

  if (x == 0) {
    myResolve("OK");
  } else {
    myReject("Error");
  }
});

myPromise.then(
  function(value) {myDisplayer(value);},
  function(error) {myDisplayer(error);}
);
```

---

# More JavaScript Promise Examples
To demonstrate the use of promises, callback examples will be used:
- Waiting for a Timeout
- Waiting for a File

# Waiting for a Timeout
Example Using Callback
```js
setTimeout(function() { myFunction("I love You !!!"); }, 3000);

function myFunction(value) {
  document.getElementById("demo").innerHTML = value;
}
```
Example Using Promise
```js
let myPromise = new Promise(function(myResolve, myReject) {
  setTimeout(function() { myResolve("I love You !!"); }, 3000);
});

myPromise.then(function(value) {
  document.getElementById("demo").innerHTML = value;
});
```


---

# Waiting for a file

Example using Callback
```js
function getFile(myCallback) {
  let req = new XMLHttpRequest();
  req.open('GET', "mycar.html");
  req.onload = function() {
    if (req.status == 200) {
      myCallback(req.responseText);
    } else {
      myCallback("Error: " + req.status);
    }
  }
  req.send();
}

getFile(myDisplayer);
```

---

Example using Promise
```js
let myPromise = new Promise(function(myResolve, myReject) {
  let req = new XMLHttpRequest();
  req.open('GET', "mycar.html");
  req.onload = function() {
    if (req.status == 200) {
      myResolve(req.response);
    } else {
      myReject("File not Found");
    }
  };
  req.send();
});

myPromise.then(
  function(value) {myDisplayer(value);},
  function(error) {myDisplayer(error);}
);
```

---

# **Javascript Async/Await**

---


# Javascript Async
In JavaScript, "async" refers to the ability to perform tasks without blocking the main execution thread. This is crucial because JavaScript is inherently single-threaded, meaning it can only do one thing at a time.   

Here's a breakdown of what asynchronous JavaScript is all about:

# Synchronous vs. Asynchronous:
- Synchronous: In synchronous programming, code is executed line by line, in a strict sequence. Each operation must complete before the next one can begin. If a synchronous operation takes a long time (like fetching data from a server), the entire program will pause and become unresponsive until that operation finishes.   
- Asynchronous: Asynchronous programming allows certain tasks to be initiated, and while they are running in the background, the JavaScript engine can continue executing other code. Once the asynchronous task is complete, a mechanism is in place to handle its result or any errors that occurred.

---

# Async Syntax

The keyword async before a function makes the function return a promise:

Example
```js
async function myFunction() {
  return "Hello";
}
```
is the same as

```js
function myFunction() {
  return Promise.resolve("Hello");
}
```
Here is how to use the Promise:
```js
myFunction().then(
  function(value) { /* code if successful */ },
  function(error) { /* code if some error */ }
);
```

---

# Await Syntax
The `await` keyword can only be used inside an `async` function.

The `await` keyword makes the function pause the execution and wait for a resolved promise before it continues:
```js
let value = await promise;
```
- Example
Basic Syntax
```js
async function myDisplay() {
  let myPromise = new Promise(function(resolve, reject) {
    resolve("I love You !!");
  });
  document.getElementById("demo").innerHTML = await myPromise;
}

myDisplay();
```
The two arguments (resolve and reject) are pre-defined by JavaScript.

We will not create them, but call one of them when the executor function is ready.

Very often we will not need a reject function.

---

- Example without reject
```js
async function myDisplay() {
  let myPromise = new Promise(function(resolve) {
    resolve("I love You !!");
  });
  document.getElementById("demo").innerHTML = await myPromise;
}

myDisplay();
```

---