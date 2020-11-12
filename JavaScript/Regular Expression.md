A regular expression is a special set of characters that allow us to match that pattern inside of a string.

In JavaScript we have two methods to create Regular Expression: the constructor method and the ...

```js
// Constructor
const regexConstructor = new RegExp('is')

// Literal
const regexLiteral = /is/;
```
It is important to remember that we are defining **a pattern** so `is` means the letter `i` followed by an `s`.

With the **literal declaration** we have to wrap the pattern with `/`.

Regular expression give us [[#Flags|some flag]] that allow us to identify additional parameters in our pattern. Little note is how we use them in the different declarations:
* **constructor** - as second parameter
* **literal** - after the closing `/`

```js
// Adding global flag
// Constructor
const regexConstructor = new RegExp('is', 'g')

// Literal
const regexLiteral = /is/g;
```

## Methods
Using this gives us useful methods to find the defined pattern:
* `test( str )` - returns a boolean based on presence of pattern in `str` 
* `exec( str )` - returns an array that will contain the founded match, the `index` for the match and the full `str` we give as `input`. These special properties [[#exec|are not easily visible in console]].

### `exec()`
Depending on browser `console.log()` will not display the special props `index` and `input` but you can always call them separately.
```js
const str = "This is a string.";
const regex = /is/;
const result = regex.exec(str);
console.log(result); // ["is"]
console.log(result.index); // 2
console.log(result.input); // This is a string. 
```
Beside this is important to note that `null` will be returned if no match has been found but also that since regex are 'state aware' we can loop all the matches if we want because if our regex has the [[#^005eb3|global]] flag each time we call `exec()` on the same string it allow us to know the different indexes.
```js
const str = "This is a string.";
const regex = /is/g;
const result = regex.exec(str);
const result1 = regex.exec(str);
const result2 = regex.exec(str);
console.log(result.index); // 2
console.log(result1.index); // 5
console.log(result2.index); // null
```
## Flags
* `g` (*global*) - allow us to keep searching for matches even if one has already found. ^005eb3
* `i` (*ignore*) - ignore the case of the char passed in the pattern 
* `m` (*multiline*) - allow us to run our regex even if the string is multiline

## String integration
Worth mention that we can work with regular expression straight from a `String` object, even this gives us some approaches to easily run and get results.
* `match( exp )` - will check the `exp` against the string and will return an array with all of the matches
* `replace( exp, fn )` - check the `exp` against the string and will let us work with the matches via the `fn` callback
* `search( exp )` - will search inside the string the first occurrence of `exp` and will return the index

```js
const str = "This is a string.";
const regex = /is/gi;

str.match( regex ); // ["is", "is"]

str.replace( regex, match => match.toUpperCase()); // ThIS IS a string. 

str.search( regex ); // 2
```
## Meta characters
They have special meaning inside a Regex:
* `.` - the dot will match any single character (letter, numbers or special) but will not match a line break
* `*` -

## Useful
`\s?` means *"potentially followed by whitespace"*
`\.` simple dot
`\|\|` double pipe `||` 