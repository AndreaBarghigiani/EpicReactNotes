Checks if an object contains any properties to define if it is empty or not.
It uses the other [[isObject]] utility function to exit early in case the value passed as argument is not an object.
```js
const isObjectEmpty = (obj) => {
  if (!isObject(obj)) return false;
  for (const prop in obj) {
    if (obj.hasOwnProperty(prop)) {
      return false;
    }
  }

  return true;
};
```