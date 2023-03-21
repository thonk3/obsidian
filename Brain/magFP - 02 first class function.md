
## Quick review
- first class functions, are just a normal class, like everything else
- treat it as a standard data type, you can 
	- store in arrays
	- pass around as function params
	- assigned to variables..
- but the world is filled with "ulge" code he said?

## Why favour first class?
- its easy to add layers of indirection, providing no added value but increasing the amount of redundant code to maintain
```js
httpGet('/posts/2', json => renderPost(json));
// if err were to add, it would need to change
httpGet('/posts/2', (json, err) => renderPost(json, err));
// if written as first class function
httpGet('/posts/2', renderPost);
```
first class functions simplify your code by making it simpler to modify, reducing redundant code
==naming== is quite an issue as well
- having multiple names for the same concept is the common source of confusion.
- having too specific name can very often lead to repeated code

## Take away
- overview of first class functions and its advantages

---
next chapter [[magFP - 03 pure functions]]