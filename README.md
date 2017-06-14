# ES6 Helper Methods

```javascript
```

## forEach


```javascript
var colors = ['red', 'green', 'blue'];

colors.forEach(function(color) {
  console.log(color);
});

// with fat arrow...
colors.forEach((color) => {
  console.log(color);
});
```

```javascript
// Create and array of numbers
var numbers = [1,2,3,4,5];

// Create a variable to hold the sum
var sum = 0;

// Loop over the array, incrementing the sum vvariable
numbers.forEach(function(number) {
  sum += number;
});

// Print the sum
console.log(sum);
```

- Optionally `numbers.forEach...` can be split into

```javascript
function adder(number) {
  sum += number;
}
// not adder()
numbers.forEach(adder);
```

## map
 
- returning new array, not mutating
- `return` is critical to be placed inside mapping function

```javascript
var numbers = [1,2,3];
var doubleNumbers = [];


var doubled = numbers.map(function(number) {
  return number * 2;
});
```

```javascript
var cars = [
  { model: 'Buick', 'CHEAP' },
  { model: 'Ford', 'EXPENSIVE'}
];

var prices = cars.map(function(car) { 
  return car.price;
});
```


