`React.useEffect()` is the Hook way that let us run some code when some state/values/props have changed. At first, when Hooks have been introduced, this looked like the answer to the [[lifecycle methods]] that we were used to use in a React class component. 

> This is very similar to [[React.useLayoutEffect()|useLayoutEffect]] with the main difference that when we use the `useEffect` Hook it gets run **after** the component renders and ensures that your effect callback does not block browser painting.

Anyway as we will dig deeper in this note `React.useEffect()` has many benefits that go over the standard lifecycle methods.
Basic syntax:
```js
React.useEffect( () => {
	// The code in here will run at each render
})
```

The `useEffect` Hook has a *dependency list*, an array that will contain the values that it needs to monitor in order to know if it has to fire or not.
```js
React.useEffect( () => {
	// The code in here will run at first render
}, [dependency, list])
```
Most of the time the items that we add to the dependency list are just variables holding values **but**, as happen for the [[2. useCallback custom hooks|useCallback exercise]] sometimes *'looks like'* we need to pass in a fn.
```js
// Custom Hook to define async operations
function useAsync( asyncCallback, initialState ){
	const [state, dispatch] = // state definition

	React.useEffect(() => {
    	const promise = asyncCallback(); // <- this is a dependency
    	// Other code not important 
	}, 
  	[asyncCallback]); // <- WRONG!!!
	
}
```
Maybe you're asking *"why should it be bad?"*

I do not mean that is *always* a bad thing, the fact is that we will need to execute our `useEffect` at each render because the `asyncCallback` we're passing, in this case, will be a *'new fn at each render'*.
```js
// How we use the custom Hook
function PokemonInfo({pokemonName}) {
  const state = useAsync(
    () => {
      // the body of the asyncCallback
    },
  // more code...
  )

```
As you can see the `asyncCallback` is defined **inside the component** and from the React point of view it'll be a new function at each render and this is not a good solution since will let us wasting resources.

In order to solve this issue we have to identify **what really changes** and pass it as a parameter to insert it in the dependencies list.

In this specific case the thing that was changing was the `pokemonName` so we changed the [[custom Hook]] declaration and it's use:
```js
// Custom Hook to define async operations
function useAsync(asyncCallback, initialState, dependencies) {
	const [state, dispatch] = // state definition

	React.useEffect(() => {
      // more code...
    }, 
	dependencies); // <- I am using the passed dependencies

  return state
}

function PokemonInfo({pokemonName}) {
  const state = useAsync(
    () => {
      // the body of the asyncCallback
    },
    // more code...
    [pokemonName], // <- this is the dependendies we pass to our custom Hook
  )
```
Probably you're using ESLint in your project, and btw congrats in doing so, and you saw the warning about dependencies of `useEffect`. To solve this you can just add a comment that will stop ESLint for the next line or use [[React.useCallback()|useCallback]] to create a [[memoize|memoized]] version of the `asyncCallback` fn.
```js
// eslint-disable-next-line react-hooks/exhaustive-deps
```
## Best benefits of `useEffect`
## Common behavior of `useEffect`
### Running at each render - without dependencies array
```js
React.useEffect( () => {
	// The code in here will run at each render
})
```
### Running after mount the component - with an empty dependencies array
```js
React.useEffect( () => {
	// The code in here will run at first render
}, [])
```
### Run when a specific prop or state changes - with a dependencies array
```js
React.useEffect( () => {
	// The code in here will run each time 'specific' changes
}, [specific])
```

## Use examples
### Set a ref to a mounted DOM node
### Make an HTTP request
### Write on localStorage
Here we are creating the [[custom Hook]] `useLocalStorageState` that is helping us save our state into the [[localStorage]] of our browser. You can see the `useEffect` Hook in action.
```js
function useLocalStorageState(key, defaultValue = '') {
    const [state, setState] = React.useState(
        () => window.localStorage.getItem(key) || 
        defaultValue,
    )
    React.useEffect( () => {
        window.localStorage.setItem(key, state)
    }, [key, state] )

    return [ state, setState ]
}
```
The dependency array hold the values for `key` and `state`, as you know, each time those values are different the `useEffect` will run.

In this example we are using the `useEffect` Hook only to save the value held in `state` inside the [[localStorage]].