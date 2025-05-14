The main purpose of XMLHTTPRequest is to make HTTP requests from the browser asynchronously without a full page refresh.

### Usage
- Create an instance with the XMLHttpRequest() constructor. 
	- `const xhr = new XMLHttpRequest()`
- to open or "fetch" a some resource with xhr
	- `xhr.open(method,url, async)`, 
		- the method can be GET, PUT, POST, or DELETE
		- the target url
		- a boolean to confirm whether the request should be asynchronous or synchronous. it is true by default.
- to actually ==send== the request after you've written it
	- `xhr.send`
- to cancel a request
	- `xhr.abort()`


#### Example
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

To illustrate how to use xhr with both callbacks and promises, look at the example below:
Callbacks
    
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


While newer event handlers like `onload` and `onerror` are often simpler, the `onreadystatechange` event is a classic way to monitor the state of an `XMLHttpRequest`.

- **`onreadystatechange` Event:** This event is fired every time the `readyState` property of the `XMLHttpRequest` object changes. By checking the value of `readyState` inside this event handler, you can track the progress of the request through its lifecycle.

The most important `readyState` value to check is `4`, which signifies that the request is `DONE` and the response from the server is ready. You typically pair this with a check of the `status` property to see if the HTTP request was successful (e.g., `status === 200`).

Here's an example using `onreadystatechange`:

JavaScript

```js
const xhr = new XMLHttpRequest();

xhr.onreadystatechange = function() {
  // Check if the request is complete (readyState 4)
  if (xhr.readyState === 4) {
    // Check if the HTTP status code indicates success (e.g., 200 OK)
    if (xhr.status === 200) {
      console.log('Data received:', xhr.responseText);
    } else {
      console.error('Request failed with status:', xhr.status);
    }
    // This handler is called multiple times (for each state change),
    // but we only process the response when state is 4.
  }
};

xhr.open('GET', '<https://example.com/data>'); // or "mycar.html"
xhr.send();

console.log('Sending request...'); // This also executes before the data is received
```

In this example, the function assigned to `onreadystatechange` will run several times as the `xhr.readyState` goes from 0 to 4. We only put our code to process the response inside the `if (xhr.readyState === 4)` block, because that's when the `responseText` and `status` properties are reliably available from the completed request.