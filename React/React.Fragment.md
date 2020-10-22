`React.Fragment` is a special component that comes built in within React that we can use instead of the common `<div>` wrapper that is commonly used to return multiple component.

Adding a `<div>` is necessary because JSX does not allow us to return multiple elements. Write something like the following is wrong.
```js
return (
	<div>Hello World</div>
	<div>Goodbye World</div>
)
```
If we want to return multiple elements in JSX, before of `React.Fragment`, we had to do like:
```js
return (
	<div className="container">
		<div>Hello World</div>
		<div>Goodbye World</div>
	</div>
)
```
This though will create an additional `<div>` that maybe we do not want to show in the resulting HTML. Since the advent of `React.Fragment` we can write something like:
```js
return (
	<React.Fragment>
		<div>Hello World</div>
		<div>Goodbye World</div>
	</React.Fragment>
)
```
This will not create a new element in our HTML but will let us add additional elements into our JSX.

Since `React.Fragment` is so commonly used, beside the ability to deconstruct it from the React main library itself, we have a shorthand way to use it:
```js
return (
	<>
		<div>Hello World</div>
		<div>Goodbye World</div>
	</>
)
```