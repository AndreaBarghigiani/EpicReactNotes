Memoize something means that we want to cache some complex calculations in order to not run the same calcs a second time if the result is the same.

The important thing to understand here is the fact that the fn used to memoize something needs to be [[Pure functions|pure]]. As a refresher a fn is defined *pure* if will return the same result if we pass the same parameters.

Simple example of a [[Pure functions|pure fn]] that we can memoize will be `addTwo`:
```js
function addTwo(input) {
  return input + 2
}
```
This function is pure because no matter what it'll return the same value if we pass the same parameter. `addTwo` will always return `5` if we call like `addTwo(3)` or will always return `3` if we call like `addTwo(1)`.

As stated before, `addTwo` is a pure fn because with the same arguments will return the same values.

If we want to memoize it we need to leverage the scope above to store the values already calculated, this way we do not have to run again the entire function we just need to return the correct value.
```js
const cache = {}
function addTwo(input) {
  if (!cache.hasOwnProperty(input)) {
    cache[input] = input + 2
  }
  return cache[input]
}
```
With this code we have produced a memoized version of our function `addTwo`. We leverage the `cache` object to store in it the calculations that we have already run.

I understand that this seems silly if we just have to *add two* to a number but this is the basic concept as since we are leveraging a variable kept outside the scope of our function generally the memoization of a function happen inside a [[Closure|closure]] so we can keep the `cache` variable *private*.

### Not only same value, same reference too
Something that not always is clear is the fact that if we store an object or an array inside the `cache` when we call it back not only we get the same value but **we also get the same reference**.