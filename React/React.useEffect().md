`React.useEffect()` is the Hook way that let us run some code when some state/values/props has changed. At first, when Hooks have been introduced, this looked like the answer to the [[lifecycle methods]] that we were used to use in a React class component. 

Anyway as we will dig deeper in this note `React.useEffect()` has many benefits that go over the standard lifecycle methods.

## Best benefits of `useEffect`
## Common behavior of `useEffect`
### Running at each render - without dependencies array
### Running after mount the component - with an empty dependencies array
### Run when a specific prop or state changes - with a dependencies array

## Use examples
### Set a ref to a mounted DOM node
### Make an HTTP request
### Write on localStorage