Return a multidimensional array of arrays where it lists all the keys (with path) and relative values.

The cool thing about it is that if the value contains an array or an object the value is stored *as is* meaning that you can loop and check for the value in complex loops. 
### Example use case
```js
// Sample object
const luke = {
  name: "Luke Skywalker",
  height: 172,
  particular: {
    hair_color: "blond",
    skin_color: "fair",
    eye_color: "blue"
  },
  custom: {
    this: {
      is_custom: true
    }
  }
};

// Use
Object.entries(luke);

// Outputs
[
  [
    "name",
    "Luke Skywalker"
  ],
  [
    "height",
    172
  ],
  [
    "particular",
    {
      "hair_color": "blond",
      "skin_color": "fair",
      "eye_color": "blue"
    }
  ],
  [
    "custom",
    {
      "this": {
        "is_custom": true
      }
    }
  ]
]
```