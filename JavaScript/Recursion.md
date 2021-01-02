Recursion is when from a function we call itself.
```js
function sillyFn( args ) {
	// More code...
	// At one point I need to call sillyFn again
	sillyFn( newArgs );
}
```
This is pretty useful when we need to work with specific data structures or when we need to repeat the same *action* with a different value.

A basic way of thinking for this pattern can be explained creating a simple `pow( num exp )` fn. To calculate an exponentiation we can programmatically solve it in two way:
* we have the *iterative* where we will use `exp` to loop and multiply `num`
* or we have the *recursive* way where we call `pwo()` itself until we reach a specific step where we'll stop

With the iterative approach we could write something like:
```js
function pow(num, exp) {
	let result = 1;
	
	// multiply result by x n times in the loop
	for (let i = 0; i < exp; i++) {
		result *= num;
	}
	
	return result;
}

alert( pow(2, 3) ); // 8
```
This is the most comforting part, we know the loop and we understand that it will exit once `i >= n`, the most difficult part (at least for me) when we talk about *recursive fn* is identify **when** I will exit from my fn.

To play with recursion you need to know when to stop.

In order to implement the same `pow()` fn with recursion we need to identify what we want from the fn, in this case, we want it to `return` the exponentiation of `num` for `exp`.

We already know that we could loop, but how it looks recursively?
```js
function pow(num, exp) {
  if (exp == 1) {
    return num;
  } else {
    return num * pow(num, exp - 1);
  }
}

alert( pow(2, 3) ); // 8
```
Here we're not using a `for` loop, here we call `pow()` **until** `exp` is not 1 (the *escape* from the function).

Basically this is what is happening when we call `pow(2, 3)`:

**First time running**
`exp == 1` so we will execute the `else` and we call again `pow()` this time with `exp` set to 2. Remember that we do not have **any value yet** so everything is still in memory.
```js
pow( 2, 2 );
```
**Second time running**
Now `exp` is `2` but the check `exp == 1` is still false so we go for the `else` once more. Here we will call again `pow()` **but** this time the value of `exp` will be `1`.
```js
pow( 2, 1 );
```
**Third time running**
Here the things get interesting... Now we are at the point that `exp == 1` will be `true` so **now we start to return some values**.
That's is one of the main point of a recursive fn, you get the value back (so you'll be able to return it) **only when** the fn reaches the *base*.

Now that `exp` is `1` we start to send back the value. The first time we do this we will just return `num` and this value will be given to the second iteration: `pow(2, 2)`.

So we can start run the math for it, remember that `pow()` is a fn that returns a numeric value, we where waiting for it and now it's time to run `num * num`, that in our simple example will be `2 * 2 = 4`.

We've executed also `pow(2, 2)` and got the value from it as well, now it's time to pass it when we where calling `pow(2, 3)`. Basically the first time we call it.

`2 * 4` this is what we need to do to get `8`, the correct value we were looking for.

Let's try to make it with code:
```js
// Calling pow( 2, 3 )
// { num: 2, exp: 3 }, different no returned yet

// Calling pow( 2, 2 )
// { num: 2, exp: 2 }, different no returned yet

// Calling pow( 2, 1 )
// { num: 2, exp: 1 }, exp == 1 returning num (2)

// Returning 2 to pow( 2, 2 )
// Before knowing the returned val
return 2 * pow( 2, 1 )
// Now we have the returned val
return 2 * 2; // 4

// Returning 4 to pow( 2, 3 )
// Before knowing the returned val
return 2 * pow( 2, 2 )
// Now we have the returned val
return 2 * 4; // 8
```

Based on those studies I created the [[allValues]] fn that leveraging the recursion let me get all the values contained in an object.