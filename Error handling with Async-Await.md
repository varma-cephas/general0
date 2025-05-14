If a promise is resolved normally, *await promise* is going to return a result, but if we get a/an rejection, *it will throw an error as if we we had a throw statement on that line*. 

In the real world though, a promise typically take some time before it rejects. In that case, there will be short delay before an error is thrown by await. We can use *try...catch*, the same way to throw a regular error.

```js
async function fnc(){
	try{
		const response = fetch(url)
	}catch(err){
		console.log(err)
	}
}
fnc();
```

In the case where we don't use *try...catch* to catch errors in our promise, we can use a *.catch* method on the function call