# ES6 notes

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

## var vs const, let

- `const` won't change over time
- `let` free to change over time - similar to `var`

```javascript
const name = 'Jane';
let title = 'Web Developer'

name = 'John'; // will throw an error - trying to reasign new value to fixed `const`
title = `Senior Web Deveoper`; // allowed to overwrite the previous title
```

## template strings / template literals

- syntactic sugar, change brought to ES6 for string interpolation

```javascript
function getMessage() {
  const year = new Date().getFullYear();

  // return "The year is " + year; <= this to be replaced with below
  return `The message us ${year}`;
}

getMessage();

```

## fat arrow functions

```javascript
// Classic function syntax
const add = function(a, b) {
  return a + b;
}

// Version with fat arrow function
const add = (a, b) => {
  return a + b;
}

// Simplified version of fat arrow function for single JS expression
const add = (a, b) => a + b;
```

- if there is just one argument ( ) parentheses can be omitted

```javascript
// Initial fat arrow function
const double = (number) => number * 2;

// Refactored, ommitted parentheses
const double = number => number * 2;
```

```javascript
// Classic map function
var numbers = [1, 2, 3];

numbers.map(function(number) {
  return number * 2;
});

// Compact map function
numbers.map(number => number * 2);
```

```javascript
// This object will throw an error as 'this' is out of of scope - undefined
// Fix 1: above teamSummary add a line => var self = this; to cache this value and replace thi inside teamSummary function
// Fix 2: on closing )}; of teamSummary change to => }, bind(this));
// FIX 3: simply changing to fat arrow function fixes the problem
const team = {
  members: ['Jane', 'Bill'],
  teamName: 'Super Squad',
  teamSummary: function() {
    // FIX 3 => return this.members.map((member) => {
    return this.members.map(function(member) {
      return `${member} is on team ${this.teamName}`;
    });
  }
};
```
- fat arrow functions make use of lexical `this`
- `this` inside the arrow function is set to context of the outside function

## enhanced object literals

- shortening **key value pairs** and **function definitions**

```javascript

// Classic way and refactoring to ES6
function createBookShop(inventory) {
  return {
    // below line can be replaced with just => inventory,
    inventory: inventory,
    // below line can be replaced with => inventoryValue() {
    inventoryValue: function() {
      return this.inventory.reduce((total, book) => total + book.price, 0);
    },
     // below line can be replaced with => priceForTitle(title)
    priceForTitle: function(title) {
      return this.inventory.find(book => book.title === title).price;
    }
  };
}

const inventory = [
  { title: 'Harry Potter', price: 10 },
  { title: 'Eloquent Javascript', price: 15 }
];

const bookShop = createBookShop(inventory);
```

## default function arguments

- way of setting up default values for arguments

```javascript
function makeAjaxRequest(url, method = 'GET') {
  return method;
  // logic to make request
}

makeAjaxRequest('google.com'); // GET
makeAjaxRequest('google.com', 'POST'); // POST - overwrites default GET
makeAjaxRequest('google.com', null); // explicitly saying null and return nothing not GET or POST, no value here will be reasigned to default
makeAjaxRequest('google.com', undefined); // reasingned to default GET 
```

## rest & spread operator
- `rest operator` captures an unlimited number of arguments e.g. numbers and putting them into single array

```javascript
// function addNumber(numbers) { <= this is replaced by below
function addNumber(...numbers) {
  numbers.reduce((sum, number) => {
    return sum + number;
  }, 0);
}

addNumbers(1,2,3,4,5,6,7,8); // instead of passing array we can pass unlimited number of arguments

```

```javascript
// another example of rest
const defualtColors = ['red', 'green'];
const userFavouriteColors = ['orange', 'yellow'];

[ 'blue', ...defaultColors, 'green', ...userFavouriteColors ];
// the end result is concatenating both arrays in to one, flattening both and pulling all element to this new one
// adding in new elements is also possible e.g. 'blue', 'green'

```

```javascript
// another example
function validateShoppingList(...items) {
  if(items.indexOf('milk') < 0) {
    return ['milk', ...items];
  } else {
    return items;
  }
}

validateShoppingList('oranges', 'milk');   // ['oranges', 'milk']
validateShoppingList('oranges', 'eggs');   // ['milk', 'oranges', 'eggs']
```

## destructuring

- by using  i.e. `{ type }` on left hand side, we are not creating object, declaring new variable 'type' and want to reference expense.type property
- to destucturing property we use `{}`, to destructure element we use `[]` e.g. `const [ name ] = companies;`

```javascript
var expense = {
  type: 'Business',
  amount: '$45 USD'
};

// var type = expense.type;
// var amount = expense.amount;

// ES6

const { type } = expense;
const { amount } = expense;

// or even simpler
const { type, amount } = expense;
```

- in another example properties can be pulled from the first object, no need to reference them by savedFile.extension etc. Also the multiple properties can be passed e.g. { encoding }

```javascript
// another example

var savedFile = {
  extension: 'jpg',
  name: 'repost',
  size: 14040
};

function fileSummary({ name, extension, size }, { encoding }) {
  return `The file ${name}.${extension} is of size ${size} and encoded in ${encoding}`;
}

fileSummary(savedFile, { encoding: 'UTF-8' });
```

```javascript
const companies = {
  'Google',
  'Facebook',
  'Uber'
};

const [ firstCompany, secondCompany, thirdCompany ] = companies;
// const [ firstCompany, ...rest ] = companies; - a way to mix in rest operator

// as oppose to old way of doing it
// var firstCompany = companies[0];
// var secondCompany = companies[1];
// var thirdCompany = companies [2];

```

```javascript
const companies = {
  { name: 'Google', 'Mountain View' },
  { name: 'Facebook', 'Menlo Park' },
  { name: 'Uber', 'San Fransisco' }
};

// [location] returns the whole first object `{ name: 'Google', 'Mountain View' }`
const [location] = companies;

// [{ location }] returns the value for the location property on first object 'Mountain View'
const [{ location }] = companies;

```

```javascript
// another example

const = {
  locations: ['Mountain View', 'NY', 'London']
}

const { locations: locations } = Google; // returns ['Mountain View', 'NY', 'London']
const { [ locations ] } = Google; // returns 'Mountain View'
```


```javascript

// example where there is no need to maintain an order when passing elements in the object, destructuring will pick up whats needed

function signup({ email, password, dateOfBirth, city, username }) {
  // code here
  // code here
};

const user = {
  username: 'myname',
  password: 'mypassword',
  email: 'myemail@example.com',
  dateOfBirth: '1/1/1990',
  city: 'NY'
};

signup(user) // passing a user object to signup function, which will take arguments in different order
```

```javascript
const points = [
  [4, 5],
  [10, 1],
  [0, 50],
];

// how to turn above to object => const pair = [{ x: 4, y:5}, { x:10, y:1 }, { x:0, y:40 }]

// map over points first
points.map(pair => {
  //destructure
  const [ x, y ] = pair;
});

// destructuring can be done directly in arguments
points.map( ([ x, y ]) => {  
  // return { x: x, y: y };
  return { x, y }; // simplified, when key/value pair is identical, can be replaced by just key - improved object literal syntax
 });

```
## classes

```javascript
class Car {
  constructor(options) {
  // constructor({ title }) { - another option with desctructuring
    this.title = options.title;
    // this.title = title; - option with desctructuring
  }

  drive() { 
    return 'vroom';
  }
}

class Toyota extends Car { // 'extends' enables to inherit from Car class
  constructor(options) { // not { color } this time as we would only pass color instead of color and title
    // super(); - if only one value is passed above in constructor i.e. { color } 
    super(options); // Car.constructor; - enables to call a constructor function on parent class e.g. Car
    // if `constructor({ color });` => `this.color = color;`
    this.color = options.color;
  }

  honk() {
    return 'beep';
  }
}

// an instance of the car
const car = new Car({ title: 'Toyota' });
car.drive();

// another instance with inheriting from parent class Car
const toyota = new Toyota({ color: 'red', title: 'Daily Driver' });
'------';
toyota.honk();
toyota.drive();
toyota;
```

## generators

### what is a generator
- function which can be entered and exited multiple times
- function which returns a value and comes back to the place where we left this off
- array helpers 'map', 'forEach' DO NOT work with generators!

```javascript
function* numbers { yield }
// or
function *numbers { yield }
```

```javascript
function* shopping() {
  // stuff on the sidewalk

  // walking down the sidewalk

  // go into the store with cash
  const stuffFromStore = yield 'cash';  // { 'value': 'cash', 'done': false }

  // walking back home
  return stuffFromStore
}

// stuff in the store
const gen = shopping(); // invoking function doesn not do anything here
gen.next(); // leaving our house
// walked into the store
// walking up and down the aisles...
// purchase our stuff

gen.next('groceries'); // leaving the store with groceries -  { 'value': 'groceries', 'done': true }

```

```javascript
// Another example of generators, for... of loop 

function* colors() {
  yield 'red';
  yield 'blue';
  yield 'green';
}

const gen = {
  gen.next(); // { 'value': 'red', 'done': false } - value returned by yield
  gen.next(); // { 'value': 'blue', 'done': false }
  gen.next(); // { 'value': 'green', 'done': false }
  gen.next(); // { 'done': false }
};

// for... of loop works really well with generators
const = [ myColors ];
for( let color of colors()) { // iterating over colors generator, running it every time colors(), next value on each call 
  myColors.push(color); // adding to the array
}

```

```javascript
// Another example

const testingTeam = { // defining the data object
  lead: 'Amanda',
  tester: 'Bill'
};

const engineeringTeam = { // defining the data object
  size: 3,
  department: 'Engineering',
  lead: 'Jill',
  manager: 'Alex',
  engineer: 'Dave',
  testingTeam // reference to testing team object
};


function* TeamIterator(team) { // returning the specific data - lead, manager, engineer
  yield team.lead;
  yield team.manager;
  yield team.engineer;
  const testingTeamGenerator = TestingTeamIterator(team.testingTeam); // team is on engineeringTeam data object which takes data from testingTeam object
  yield* testingTeamGenerator; // will return all values via testingTeamGenerator const
}

function* TestingTeamIterator(team) {
  yield team.lead;
  yield team.tester;  
}

const names = [];
for(let name of TeamIterator(engineeringTeam)) { // iterating over passing data object to iterator which yields data specified in generator
  names.push(name);
}

```

### symbol iterator

```javascript
// REFACTORING of the above code...   Symbol.iterator and for...of loop
 
const testingTeam = { // defining the data object
  lead: 'Amanda',
  tester: 'Bill',
  [Symbol.iterator]: function* () { // a way to tell how this data object should be available to yield* for iteration for..of loop
    yield this.lead; 
    yield this.tester;
  }
};

const engineeringTeam = { // defining the data object
  testingTeam, // reference to testing team object
  size: 3,
  department: 'Engineering',
  lead: 'Jill',
  manager: 'Alex',
  engineer: 'Dave',
  [Symbol.iterator]: function* () { // a way to tell how this data object should be available to yield* for iteration for..of loop
    yield this.lead;
    yield this.manager;
    yield this.engineer;
    yield* this.testingTeam; // yield value is another generator function so * kick in iteration over in testingTeam [Symbol.iterator]
  }
};

const names = [];
for(let name of engineeringTeam) { 
  names.push(name);
}

```

### tree data structure, for..of loop application, generators with recursion

```javascript

// data structure 

class Comment {
  constructor(content, children) { // passing content value and array of children
    this.content = content;
    this.children = children;
  }

  *[Symbol.iterator]() { // improved object literals syntax, how to write inside a class
    yield this.content;
    for(let child of this.children) { 
      yield* child;
    }
  }
}

const children = [
  new Comment('good comment', []),
  new Comment('bad comment', []),
  new Comment('okay comment', []),
  new Comment('meh....', [])
];

const tree = new Comment('Great post!', children); // like in thread this is parent comment, displaying children comments below

// iteration over data structure

const values = [];
for(let value of tree) {
  values.push(value);
}

```


