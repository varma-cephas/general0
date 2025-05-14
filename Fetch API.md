### Introduction
The fetch API is mostly used for sending a **HTTP Request** and returning a **Promise** that resolves a **Response object** which contains the resource that was requested for. **Fetch** was created to be a modern replacement for **[`XMLHttpRequest`](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest)** way of making **HTTP Requests** and getting processing response .
	- Unlike **XMLHttpRequest** which uses callbacks, **Fetch** is *promise based*.
We can make request with **Fetch** by using the `fetch()` function, which returns a **promise**.
	- The `fetch()` function  one compulsory method, the URL or endpoint to the resource that we're trying to fetch, with two other two optional parameters:
```js
fetch("https://api.example.com/data")
  .then(response => response.json())
  .then(data => {
    console.log(data);
  });
```

 the **Fetch API** also provides methods that we can use to format various response outputs, such as 
	 - `.json()` for parsing our response data in a JSON format
	 - `.text()` for parsing our response data in a text format
	 - `.arrayBuffer()` in an ArrayBuffer
	 - `.blob()` in a Blob

It is useful to remember that **Fetch API** is primitive or low level by design, and it doesn't have a built-in way to send data formats like *JSON* or *FormData*, it rather provides building blocks for us to implement these features ourselves.

### Post request 
Since the default *request method* used in the **Fetch API** is **GET**, if we want to use other **HTTP methods** like **POST, PUT, or DELETE**, we have to explicitly define those in the `fetch()` function.
```js
fetch("https://api.example.com/data", {
  method: ‘POST‘,
  headers: {
    ‘Content-Type‘: ‘application/json‘
  },
  body: JSON.stringify({ message: ‘Hello, world!‘ })
})
```
In the example above, we are making **POST request** with a **JSON payload** in the **request body**. We set the `Content-Type` to `application/json` to indicate that *we're sending JSON data* 

## Auth
A lot of APIs requires authentication before accessing it's resources, and the **Fetch API** provides multiple ways to include those *authentication credentials* in your requests.

The easiest way to do this is to include an *Authorization header* in the request you are making:
```js
fetch("https://api.example.com/data", {
  headers: {
    ‘Authorization‘: ‘Bearer my-access-token‘
  }
})  
```
While this works for **JWT or OAuth**, there are APIs that uses **cookie-based authentication**. If that is the case, you can use:
```js
fetch("https://api.example.com/data", {
  credentials: ‘include‘  
})
```

## Uploading files

The **Fetch API** makes it extremely easy to upload files as a part of the **POST or PUT** request. To go about doing this, you can create a *FormData object* , and append the multiple or a single file to it.
```js
const formData = new FormData();
formData.append(‘image‘, imageFile);

fetch("https://api.example.com/upload", {
  method: ‘POST‘,
  body: formData
})
```
When using **Form Data**, we  don't need to set the *Content-header* explicitly, because the browser will set it to automatically set it to *multipart/form-data* and handle the encoding data.