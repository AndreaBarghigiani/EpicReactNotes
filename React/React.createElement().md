The `createElement()` method takes two params:
* `element` - a string representing the HTML element that we want to create
* `props` - a JS object that will keep all the information needed to render the element (id, class, text...)

A basic creation of a React element is:
```js
React.createElement( 'div', {
	className: 'container',
	children: 'Hello World'
})
```

The `children` are the content of the element, it could be a string or any other elements.

Beside that the `children` is a special `prop` in React and you can pass it any number of children after the prop declaration, basically this snippet:
```js
React.createElement( 'div', {
	className: 'container',
	children: ['Hello', ' ', 'World']
})
```
Is equal to:
```js
React.createElement( 
	'div', 
	{ className: 'container'},
	'Hello', ' ', 'World'
)
```
In both cases I am passing multiple elements within an array but in the first one it is explicit in the second one is React doing it's magic. If you `console.log()` the element you'll find out that both have the same structure.

If I need to pass down more DOM elements I need to create them first:
```js
// If I do not need props they could be null or empty obj
const spanHelloElement = React.createElement( 'span', null, 'Hello')
const spanWorldElement = React.createElement( 'span', {}, 'World')
const reactElement = React.createElement( 
	'div', 
	{ className: "container" }, 
	spanHelloElement, ' ', spanWorldElement 
);
	
ReactDOM.render( reactElement, rootElement )