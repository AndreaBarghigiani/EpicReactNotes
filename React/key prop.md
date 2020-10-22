The `key` prop is a special functionality in React that helps the library understand what has changed in a generated JSX. I am talking about generated JSX because the following list are different even if the output HTML looks the same.
```js
// Assume we are inside a component

// I am returning a full list
return (
	<ul>
		<li>One</li>
		<li>Two</li>
		<li>Three</li>
	</ul>
);

// I am generating the list of li elements with .map() that generates a new array
const elements = [ 'One', 'Two', 'Three' ];
<ul>
	{elements.map( el => <li>{el}</li>)}
</ul>
```
The main difference here is that for React the first example is just a [[React.createElement()]] with HTML in it instead the second one is an array that generates an element, calls [[React.createElement()]], for each item.

In order to help React know which element we are working with is always a best idea to add an unique `key` prop that also helps it increase the performances of our code, besides removing some silly errors when React guess badly 😉

When using `key` prop is best practice **not use an index** because need to be consistent for the component for the component that React is tracking, the index of an array follows the position of an item and that's means that different value can have the same position between renders based on how we remove/add the data in the array.