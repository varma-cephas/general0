 While it’s possible to have multiple `.then()` ’s chained together, only the first `.catch` method will be fired when a promises encounters an error, except when the first catch throws an error.
- Only one function can be added to the callstack at a time
    - after one function is added to the stack, any another function that is in that function is going to be poped onto the stack to be executed.
    - **Stacks** as a data-structure followed the LIFO (last in first out) principle,
- When a task is done, setTimeout for example, the `Web API` doesn’t not send it to the call-stack, because it has no or little influence over the call-stack. It rather sends it to the `Task Queue` .
    - The `Task Queue` stores jobs or callbacks that comes from async async operations.
        - The `Task Queue` operates on a FIFO basics (first in, first out).
- For things to get executed that are on the `Task Queue`, it needs to placed onto the call-stack, and this is where the `Event Loop` comes into play.
- `Event loop` is a mechanism which checks the call-stack when it’s empty, and looks inside the `Task Queue` for things that have been **queued** up for execution after all the synchronous code has been executed.
    - The `Event loop` is constantly running in the background to check if the call-stack is empty.
- When JavaScript comes across an `Event listener` , it takes take event listener, pops it onto the call-stack, since the browser don’t know when that event will happen, it is passed off to the WebAPI, and when that event is triggered, it get’s popped onto the `Task Queue` , which waits patiently for the `Event loop` , which keeps checking if the `Call Stack` is free. When it is, the callback is then passed onto the call-stack for execution.
- A function declared with the async keyword will always return a promise, regardless if it’s awaiting an asynchronous operations or not.

# 4.30.25, JS Callbacks

- JavaScript function are executed in the sequence in which they are `called` and not by how they are defined.
    
- By definition, a callback is a function that is passed as an argument to another function.
    
    - _when passing a function as an argument, do not use a parenthesis_
- Where callbacks shines are in asynchronous function, when one function has to wait for another function, (like wait for a network request for example).
    
- Callbacks can be called in two ways, **synchronous** and **asynchronous**.
    
    - **Synchronous callbacks** are called immediately after the invocation of the outer function or the higher order function.
    - **Asynchronous callbacks** on the other hand are called at some point later, after an asynchronous operation has completed.
    
    ```jsx
    let value = 1;
    
    doSomething(() => {
      value = 2;
    });
    
    console.log(value);
    ```
    
    in the example above, the `doSomething` function is taking a synchronous callback as an argument, so `value` is going to be `2` instead of `1` . If the callback was asynchronous on the hand, the `value` would be `1` instead of `2` .
    
    - Examples of synchronous callbacks includes array methods like `.map()` , `.forEach()`
    - Examples of asynchronous callbacks includes `setTimeout()` , `Promise.then()`
- XMLHttpRequest demo, using event based pro
    
    ```js
    const xhr = new XMLHttpRequest();
    xhr.onload = function() {
      console.log('Data received:', xhr.responseText);
    };
    xhr.onerror = function() {
      console.error('Request failed');
    };
    xhr.open('GET', '<https://example.com/data>');
    xhr.send();
    
    console.log('Sending request...'); // This also executes before the data is received
    ```
    
- Functions **running in parallel** with other functions are called asynchronous function. An excellent example of this is `setTimeout` . When passing a function to `setTimeout` , remember to not use a parenthesis.
    
- Another asynchronous function `setInterval` is used to fun a certain function after a specific interval of time.
    

## Callbacks alternatives

- While it might be good for some use cases to use callbacks when dealing with asynchronous operations, it can easily become difficult to write and debug.
- To fix this issue, **Promises** can be used.

## An asynchronous function using callbacks vs promises

- Callbacks
    
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
    
- Promises
    
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
    

# 4.29.25, Promise.all

- the `Promise.all()` method takes an array of promises, executes them, and returns an array of values in the same order was the array of promises. `Promise.all()` fails fast because it will reject as soon as the first promise rejects, without waiting for the rest of the other promises to settle. This means that even if one promise gets rejected, the entire array of promises gets rejected. If everything resolves successfully, then the next `.then()` method gets the chain of values.
- `Promise.all()` allows us to run all of the promises passed to into the array all at once.

# 4.23.25, Gap year retrospective

- Remove phone numbers and name and share the google sheets
- The group are divided into two, this coming Saturday is going to be for the one week ahead, and the next is going to be one session for the people one week ahead and another for the one week behind people.
- Send emails to the week one ahead ahead about the list: From now on you guys will be at this location, from the one week ahead, so please be there on Saturday, and be on time, before one so that they will be ready. Emphasize on telling them to come at least 20 mins before.
    - communicating to them that they have been moved. the people on discord are the ones who came during last weekend. the google sheet are the people who showed up. Emphasize on people reacting to messages. Overcommunicate. Copy the emails, letting them know that they’re move to the one week ahead group, and go on discord and let them know that we had made some changes.
    - tell the participants to always react to messages and people who still have their profiles in numbers. tell people who has double accounts to use only one account.
    - three session on weekends, combine everybody who came for the evening sessions. The two session will happen on Sunday. The morning session is going to be the one week behind, and evening will be one week ahead. The evening will be the one week ahead group.
    - slight adjustment: those people who want to attend the evening who are in the one week behind, can tell the coaches that they’re in the one week behind group, so that we can place them in a seperate room and allow them to do the session. `We can ask the people who are one week ahead in a separate rooms and then they can do their hours. one week behind in the morning and one week ahead in the evening.`
    - keep room for making slight adjustment as we go one. last weekend we invited 500 people. Be flexible with the participants. keep in mind that we’re not offering them food, so if they can keep up, let them do the entire day. let them know that we’re not offering food. the training is intended to happen six to ten hours.
        - they will not progress if they only spent 6 on the weekend. next week, only people who did not attend the last session is going to attend the morning session.
- A new sheet has been created with the time and location of the coaching program.
- Week leads can create a meeting and invite the coaches and . task is to follow up and keep remind people to check their emails and react to messages.

# 4.23-25.25, Asynchronous JavaScript: Promises

- Multiple `.thens` can be chained when working with promises. You can return the value obtained from one promise into another `.then` and on and on.
    
    ```jsx
        getJSON('../data/earth-like-results.json')
        .then(function(response){
          addSearchHeader(response.query);
          console.log(response.query);
          return response.results
        }).then(function(url){
          console.log(url[0])
        })
    ```
    

# 4.14-16.25, Asynchronous JavaScript: Promises

There are multiple ways to implement asynchronous operations in JavaScript, but **Promises** are often considered a highly effective method.

**Why should Promises be used instead of other methods when implementing asynchronous operations in JavaScript?**

Promises should be used because they provide several key advantages:

- **Flexibility:** They offer a flexible way to handle the eventual result of an asynchronous operation.
- **Easy-to-use Syntax:** Promises provide a cleaner and more manageable syntax compared to traditional callback patterns, especially when dealing with multiple asynchronous operations (avoiding "callback hell"). This is further enhanced by `async/await` syntax built upon Promises.
- **Error Handling:** They have built-in mechanisms (`.catch()`) for centralized and more straightforward error handling for asynchronous code.

## Callbacks (Historical Context)

Before **`Promises`** became the standard method, **callbacks** were the primary mechanism for managing asynchronous operations in JavaScript. To execute code _after_ an asynchronous task finished, you had to pass a function (the callback) to be called upon completion. When dealing with multiple dependent asynchronous steps, this often led to deeply nested and hard-to-read code structures, commonly known as "callback hell".

## Understanding Promises

A **`Promise`** is a fundamental object in asynchronous JavaScript. It acts as a placeholder for a value that is initially unknown but expected in the future, typically resulting from an asynchronous operation (like a network request or timer).

A `Promise` exists in one of three states:

1. **Pending:** The initial state; the asynchronous operation is still ongoing.
2. **Fulfilled (Resolved):** The operation completed successfully, and the `Promise` now holds the resulting value.
3. **Rejected:** The operation failed, and the `Promise` holds information about the error.

`Promises` come with methods, primarily `.then()` and `.catch()`, which allow you to attach callbacks that will execute when the `Promise` is either fulfilled or rejected, respectively. This provides a cleaner, more manageable way to handle asynchronous results and errors compared to traditional nested callbacks.

## Asynchronous Execution Model & Promises

Using `Promises` does **not** change the fundamental asynchronous nature of JavaScript or make operations execute synchronously. JavaScript operates primarily on a **single main thread** alongside an **event loop**.

When you initiate an asynchronous operation that returns a `Promise`, the operation runs in the background (e.g., waiting for a network response). This allows the main thread to continue executing other code, keeping your application responsive. The event loop ensures that the functions attached via `.then()` or `.catch()` are executed only _after_ the `Promise` settles (is fulfilled or rejected) and the main thread is available.

## Unpredictable Completion Order

A key characteristic of asynchronous operations, even when managed by `Promises`, is that their **completion order is not guaranteed** based on when they were started.

- You must assume you **do not know** the exact moment an asynchronous operation will finish and its `Promise` will settle.
- **Example:** If you start two network requests using `Promises` (Request A and Request B) around the same time, you cannot assume Request A's `Promise` will fulfill before Request B's. Factors like network latency or server processing time mean Request B might complete first. If a specific order is required, you must explicitly enforce it, often by chaining `Promises` (starting the second operation within the `.then()` callback of the first).

## Asynchronous operations.

Many operations in JavaScript are inherently asynchronous and are commonly handled using `Promises`:

- **Network requests** (e.g., using the `Workspace` API)
- **Timers** (`setTimeout`, `setInterval` - can be wrapped in `Promises` for easier handling)
- **File system operations** (especially in environments like Node.js)
- **Database queries**
- Responding to **Events** (like user interactions, although direct event handling often uses event listeners, Promises can be used to manage asynchronous tasks triggered by events)

## Handling Asynchronous Code with Promises

**`Promises`** are the standard and preferred way to manage asynchronous operations in modern JavaScript (prior to the introduction of syntax built upon them). They offer significant advantages:

- **Improved Readability:** Avoid "callback hell" through chaining with `.then()`.
- **Better Error Handling:** Centralized error handling using `.catch()`.
- **Composition:** Easier to combine and manage multiple asynchronous operations (e.g., using `Promise.all()` or `Promise.race()`).

## Asynchronous Operations Defined

**Q: What are asynchronous operations?**

> A: Asynchronous operations are operations that happen at an unknown or unpredictable time relative to the main flow of program execution. Their completion doesn't occur immediately.

**Q: What are some examples of asynchronous operations?**

> A: Common examples include:
> 
> - Network requests
> - Events (like user clicks, mouse movements)
> - Timers (`setTimeout`, `setInterval`)
> - File system operations (in Node.js)
> - And others where the result isn't available instantly.

## Callbacks Explained

Callbacks are a fundamental strategy for handling asynchronous work in JavaScript, particularly common before `Promises` became widespread.

- **Mechanism:** The core idea is passing one function (the callback) into another function that performs an asynchronous task. This callback function is designed to be called _later_, once the asynchronous task completes or meets certain conditions. The result of the task (or an error) is often passed as an argument to the callback function.

**Challenges and Considerations with Callbacks:**

While callbacks allow asynchronous operations, they present significant challenges:

1. **Error Handling:**
    - It's crucial to assume that any asynchronous operation might fail (e.g., network request errors).
    - This raises questions: If an error occurs, should the primary callback still be invoked? How do you differentiate between JavaScript errors within the callback logic and errors from the asynchronous operation itself (like a network error)?
    - While not strictly mandatory by the language, implementing a robust error handling strategy for callbacks is essential, but the responsibility falls entirely on the developer. Conventions like the "error-first" pattern (where the callback's first argument is reserved for an error object) were developed to standardize this, but they are just conventions.
2. **Callback Hell (Pyramid of Doom):**
    - Consider scenarios where you need multiple asynchronous operations to run sequentially, with each step depending on the previous one.
    - Using callbacks often requires nesting them: the callback for the first operation initiates the second, whose callback initiates the third, and so on.
    - `asyncOp1(result1 => { // Callback 1 asyncOp2(result1, result2 => { // Callback 2 asyncOp3(result2, result3 => { // Callback 3 // ...and so on }); }); });`
    - This deep nesting becomes extremely difficult to read, maintain, and debug. This pattern is famously known as **"Callback Hell"** or the **"Pyramid of Doom"**.
3. **Debugging and Maintainability:**
    - The nested structure resulting from callbacks makes tracing logic and debugging significantly harder compared to more linear asynchronous patterns. Maintenance becomes complex as logic gets buried deeper.

Q: What is the difference between a callback and a promise?

**A:** A callback is a function that is passed to another function to carry out some operation at a later stage, when certain conditions are met. While a promise, on the other hand, is an object that is used to carry out asynchronous operations.

## Dealing with Promises

Working with promises can be divided into the following steps:

1. **Constructing the promise using `new Promise()` syntax:**
    - `new Promise((resolve, reject) => { ... });`
    - `resolve`: Function to call if the asynchronous operation is successful.
    - `reject`: Function to call if the asynchronous operation fails.
2. **Reacting to the promise resolution:**
    - `.then()`: Used to handle the successful resolution of a promise. It receives the resolved value as an argument.
    - `promise.then(value => { /* handle successful result */ });`
3. **Handling any errors that may arise:**
    - `.catch()`: Used to handle errors that occur during the promise execution or in the `.then()` handlers. It receives the error as an argument.
    - `promise.catch(error => { /* handle error */ });`
4. **Chaining multiple promises:**
    - Promises can be chained together, where the result of one promise is passed to the next `.then()` handler. This allows for sequential asynchronous operations.
    - `promise1.then(value1 => { ... return promise2; }).then(value2 => { ... });`

## Promise States (usually describes four actions):

- **a. fulfilled (resolved) - success :)**
- **b. rejected - it did not work :C**
- **c. pending - waiting, has not been resolved or rejected :|**
- **d. settled - something happened :o**

## Working with the Promise Constructor

When working with the promise constructor, two methods are mainly used: `resolve` and `reject`. The `resolve()` method can only be called once; if it is called twice, nothing happens the second time.

Meaning that a promise can only settle once. Once a promise is either resolved or rejected, any subsequent calls to `resolve()` or `reject()` will be ignored.

Promises are not a one-size-fits-all for long-running operations; there is a technique for chaining. You can think of them as try-catch wrappers around asynchronous work.

## Promise Constructor

- A promise is a try-catch wrapper around code that will finish at an unpredictable time.
- A promise is a constructor, meaning that you can actually store it in a variable or use `new`.
- Promises take one function as an argument, which has two parameters: `resolve` and `reject`.
- `resolve` and `reject` are two callbacks that are used to signify if a promise has been resolved or rejected.
- The promise does not necessarily stop when `resolve` is called. Any value that is passed to `resolve`...

If there is an error in the body of the promise, the `catch` part of the promise gets called. While you can only have one `resolve` in a promise, that does not mean that the other code after `resolve` in the scope of the inside of a promise...