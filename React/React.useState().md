Accept a value that will be used to set the initial state of our custom component, this functions returns two values in an array:
1. the first value will be the value of the state at the current time we're calling it
2. the second value is a function that will let us update the state

React returns those two values in a form of an array and generally we [[destruct]] those to make simplier to access and use them later.
```js
// Here I define a new state called state, to update it I'll use setState()
// and it's initial value will be 0
const [ state, setState ] = React.useState(0);
```
State can be defined as: data that changes over time.

Each time the state of a component gets changed React will render the component to update the UI with the new information.

## Performance tip
The `useState` Hook will get called each time a component render (and re-renders) and if we use some complex functions or if we have to rely on API to calculate the initial value of our state this could be a problem because the function that we use **get's called each time**.

To avoid this instead of passing the function call that calculates the initial value for the state we can pass it within a function to let React call it only the first time a component gets rendered.

```js
function someComplexCalcs(){
	// Your complex calcs to generate the initial value
}

// We call someComplexCalcs() each time component renders or re-renders
const [state, setState] = React.useState(someComplexCalcs())

// We execute someComplexCalcs() only once at first render
const [state, setState] = React.useState( () => someComplexCalcs())
```
This approach is called *lazy initialization* and will save us from bottlenecks in our app on sequential renders.