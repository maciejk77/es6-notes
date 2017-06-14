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
  { model: 'Buick', price: 'CHEAP' },
  { model: 'Ford', price: 'EXPENSIVE'}
];

var prices = cars.map(function(car) { 
  return car.price;
});
```

## filter

- similar to map, `return` is required to return filtered value(s)

```javascript
var products = [
  { name: 'cucumber', type: 'vegatable' },
  { name: 'banana', type: 'fruit' },
  { name: 'celery', type: 'vegetable' },
  { name: 'orange', type: 'fruit' }
];

products.filter(function(product) {
  return product.type === 'fruit';
});
```

```javascript
var products = [
  { name: 'cucumber', type: 'vegatable', quantity: 0, price: 1 },
  { name: 'banana', type: 'fruit', quantity: 10, price: 15 },
  { name: 'celery', type: 'vegetable', quantity: 30, price: 13 },
  { name: 'orange', type: 'fruit', quantity: 3, price: 5 }
];

// Type is vegetable, quatity is greater than 0, price is less than 10
products.filter(function(product) { 
  return product.type === 'vegetable' 
    && product.quantity > 0 
    && product.price < 10;
});
```

```javascript
var post = { id: 4, title: 'New Post'};

var comments = [
  { postId: 4, content: 'awesome post' },
  { postId: 3, content: 'it was okay' },
  { postId: 4, content: 'neat' },
];

function commentsForPost(post, comments) {
  return comments.filter(function(comment) {
    return comment.postId === post.id;
  });
}
```

## find

- i.e array iterator returns true/false, once true is return immediately leaves array iteration, no need to break out from it like in the `for` loop with `break` statement 
- `return` is also required as in `map`, `filter`

```javascript
var users = [
  { name: 'Jill' },
  { name: 'Alex' },
  { name: 'Bill' }
];

users.find(function(user) {
  return user.name === 'Alex';
});
```

```javascript
var posts = [
  { id: 1, title: 'New Post' },
  { id: 2, title: 'Old Post' }
];

var comment = { postId: 1, 'Great Post' };

function postsForComment(posts, comment) {
  return posts.filter(function(post) {
    return post.id === comment.postId;
  });
}

```

## every & some

- `every` logic: False && True && False => false (iterator check whether every given element of the computer array meet the criteria, if not returns => false)

```javascript
var computers = [
  { model: 'Apple', ram: '24' },
  { model: 'Compaq', ram: '4' },
  { model: 'Acer', ram: '32' },
];

computers.every(function(computer) {
  return computer.ram > 16;
});

```

- `some` logic : True || False || True => true (iterator check whether some elements of computer array (at least one in our example) meet the criteria and returns => true)
```javascript

computers.some(function(computer) {
  return computer.ram > 16;
});

```

## reduce

```javascript
var numbers = [10, 20, 30];
var sum = 0;

// reduce helper returns current sum add a number from array and returns new sum 
// until all elements of numbers array will be iterated over, `...}, 0);` 
// zero here is the starting point as per `var sum = 0;` declaration 
numbers.reduce(function(sum, number) {
  return sum + number;
}, 0);
```

```javascript
var primaryColors = [
  { color: 'red' },
  { color: 'yellow' },
  { color: 'blue' }
];

// previous is and array start at [] as per `...}, [])`
primaryColors.reduce(function(previous, primaryColor) {
  // previous array is being updated by reduce iterator
  previous.push(primaryColor.color);

  // previous array has to be returned after each iteration to be available as a new previous value
  return previous;
}, []);
```

```javascript
// balanced () problem - the example of application of reduce
// Question: given the string which contain some number of parenthesis, are the expression correctly balanced?
function balancedParens(string) {
  // ! flips the condition into truthy true or false from numeric value
  return !string.split("").reduce(function(previous, char) {
    if(previous < 0) { return previous; } // covers the edge case balancedParens(')(');
    if(char === '(') { return previous++; }
    if(char === ')') { return previous--; }
  }, 0);  
}

// unbalanced returns => true or false
balancedParens('(((())))');
```






