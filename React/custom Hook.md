A custom Hook is a normal JavaScript function that wrap shared logic between components. What makes a custom Hook a custom Hook is:
* the fn name **must** start with `use`, this is just a best practice that if not followed will thrown an error
* it **must** use other Hooks in it and this is what accounts for 'shared logic'

Create a function is basic JavaScript stuff and something we do each single day, always remember that even if we're using React here a custom Hook is nothing less nothing more than a function.

So the first thing we do to solve our problem is to create the function that will contain the shared logic:
```js
function useLocalStorageState(){
	// Shared logic
}
```
Once we have the function we need to start thinking about the logic that we want to put in it. 

As highlighted a custom Hook has to use other build-in Hooks in order to be one. For example, if you need to wrap the logic that is getting a value and stores it in `localStorage` we can write something like this:
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
As we can see this custom Hook `useLocalStorageState` gets two parameters:
* a `key` that will identify the value stored in `localStorage`
* a `defaultValue` that we initialize with an empty string and will identify the value that we need to store in `localStorage` for the specified string

Note that this custom Hook is behaving similarly to the built-in [[React.useState()|useState]] Hook since is returning an array where the first value is the actual value of the state and the second one is the updater fn.

Once this custom Hook is in place and imported within our component we can start to use it as follow:
```js
// State with localStorage for the name
const [name, setName] = useLocalStorageState('name', 'Andrea')
// State with localStorage for the age
const [age, setAge] = useLocalStorageState('name', 37)
```
### Other examples
...