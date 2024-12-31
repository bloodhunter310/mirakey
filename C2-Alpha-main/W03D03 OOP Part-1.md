# OOP In JavaScript

## High Level Goals

By the end of this lesson, you will be familiar with the following:

- The definition OOP
- Using Methods
- Using the keyword `this`
- Design patterns and inheritance

## Object Oriented Programming

### What Is OOP

Object-oriented programming is based on the concept of "objects", which can contain data, often known as attributes or properties, and code, in the form of procedures often known as methods.

There are many object oriented programming languages such as Java that support all of it's functionality such as creating `classes` and `inheritance` but when it comes to JavaScript things work different since it isn't a class based object-oriented language but it still manage to provide
another way to do OOP since it is a prototype-based language.

JavaScript is full of objects to the point that almost everything is an object or behaves like one for examples primitives like strings are not objects but it is possible to use methods on them.

A basic OOP example:

```js
const getInformation = function () {
  // using the keyword `this` we can reference the correct instance that is invoking this function
  return (
    "name: " +
    this.name +
    "\n position: " +
    this.position +
    "\n salary: " +
    this.salary
  );
};

// we can use the employee function to create employee instances (objects)
const Employee = function (name, position, salary) {
  const emp = {};

  // add all variables along side methods as key value pairs in the emp object
  emp.name = name;
  emp.position = position;
  emp.salary = salary;

  // we took the function definition outside so we don't have to redeclare the same functions every time a new object is instantiated
  emp.getInformation = getInformation;

  // returns an object that represents an employee
  return emp;
};

const emp1 = Employee("John", "Junior developer", 1000);

// the `this` inside `getInformation` will refer to the instance/object invoking the method which is usually whatever is on the left of the dot.
emp1.getInformation(); // => name: John
// => position: Junior developer
// => salary: 1000
```

Examples on keyword `this`

```js
// in the console try to the following
this;
// when used in the console `this` will refer to the Window object and that holds the globals scope and built in methods and more
const someVar = this;
const someFunc = function () {
  return this;
};

const anotherFunc = function () {
  setTimeout(function () {
    console.log(this);
  }, 1000);
};

const obj = {
  a: this,
  b: someVar,
  c: someFunc,
  d: anotherFunc,
};

// both values would refer to the window object
obj.a;
obj.b;

// invoking some func will return the window object
someFunc();

// invoking someFunc by an object will result in `this` to refer to the object it self
obj.c();

// inside setTimeOut `this` would refer to the window object
// any callback function will return the window object
obj.d();
```

### Design Patterns

Design patterns are reusable solutions to commonly occurring problems in software design, there are mainly three types `Creational`, `Structural`, and `Behavioral`.

We will mainly look into some of the creational design patterns for JavaScript, mainly to introduce the `new` keyword and to preform object inheritance.

#### Constructor Design Pattern

```js
const getName = function () {
  return "name: " + this.name;
};

const Person = function (name, age) {
  // instead of creating a new object, just add `this` instead of the object name

  this.name = name;
  this.age = age;

  this.getName = getName;

  // no need to return anything, `this` gets returned by default when using `new`
};

// the `new` keyword will create a new instance of Person
const person1 = new Person("John", 27);

person1.getName(); // => name: John
```

#### Prototypal Design Pattern

```js
const Car = function (brand, year, price) {
  this.brand = brand;
  this.year = year;
  this.price = price;
  // remove the methods from the constructor function
};

// attach the method to the prototype object
Car.prototype.getPrice = function () {
  return "price: " + this.price;
};

// the `new` keyword will create a new instance of Car
const car1 = new Car("Toyota", 2019, 10000);

car1.getPrice(); // => price: 10000
```

```js
// it is possible to modify existing functionality in global objects like Array that are used in construction of arrays
Array.prototype.getFirstItem = function () {
  // `this` refers to the array that is invoking the method
  return this[0];
};

Array.prototype.sumSlice = function (start, end) {
  let sum = 0;
  const slicedArray = this.slice(start, end);

  slicedArray.forEach(function (element) {
    sum += element;
  });
  return sum;
};

// [10, 2, 5].getFirstItem(); // => 10
// [10, 2, 5].sumSlice() // => 17
// [10, 2, 5].sumSlice(0, 2) // => 12
// [10, 2, 5].sumSlice(1, -1); // => 2
```

### Inheritance

Inheritance the process of copying methods and attributes from one object to another.

Example on inheritance

```js
const Animal = function (name) {
  this.name = name;
};

// define a method for Animal
Animal.prototype.getName = function () {
  return this.name;
};

const Reptile = function (name, hasLegs) {
  // use the parent constructor(Animal) and pass `this` (Reptile) alongside the parent properties
  Animal.call(this, name);
  // define the child properties below
  this.hasLegs = hasLegs;
};

// inherit the `Animal` prototype, `Reptile` has `getName` now
Reptile.prototype = Object.create(Animal.prototype);

// set the `Reptile` constructor to 'Reptile' otherwise it would have been the `Animal` constructor
Reptile.prototype.constructor = Reptile;

// define a method for Reptile
Reptile.prototype.hasLegs = function () {
  return this.hasLegs;
};

const Snake = function (name, isPoisonous) {
  // pass the Snake instance to the parent (Reptile)
  // since snakes don't have legs then we could just pass the value directly without getting it from a parameter
  Reptile.call(this, name, false);

  this.isPoisonous = isPoisonous;
};

// inherit the `Reptile` prototype, `Snake` has `getName` and `hasLegs` now
Snake.prototype = Object.create(Reptile.prototype);

// set the `Snake` constructor to 'Snake' otherwise it would have been the `Reptile` constructor
Snake.prototype.constructor = Snake;

Snake.prototype.isDangerous = function () {
  return this.isPoisonous;
};

const medusa = new Snake("Medusa", true);

medusa.getName(); // => "Medusa"
medusa.hasLegs(); // => false
medusa.isDangerous(); // => true
```

### Pulse Check

1. Write a function `Human` that returns an object with the following attributes, `name`, and `age`.

   ```js
   const Human = function (name, age) {
     // TODO: Your code here
   };

   const human1 = Human("John", 24);
   human1; // => { name: 'John', age: 24 }
   ```

2. Modify `Human` to use constructor pattern.

   ```js
   const human2 = new Human("Jane", 25);
   human2; // => { name: 'Jane', age: 25 }}
   ```

3. Add a method `introduce` to the `Human` object, that returns a string introducing the person.

   ```js
   const human3 = new Human("Mark", 30);
   human3.introduce(); // => "Hello I am Mark"
   ```

4. Modify `Human` to use prototypal design pattern when it comes to it's methods.

   ```js
   // make sure the method is part of the prototype for the `Human` object
   const human4 = new Human("lilly", 30);
   human4.introduce(); // => "Hello I am lilly"
   ```

5. Write a function `Parent` that inherent from `Human` the base attributes, and adds to them a new attribute `hasChild`.

   ```js
   const Parent = function (name, age, hasChild) {
     // TODO: Your code here
   };

   const parent = new Parent("Alex", 41, true);
   parent1.hasChild; // => true
   ```

### Practice

1. Write a constructor function `Safe` that accepts one argument `safeSize` and returns an object with the `safeSize` attribute and a method called `insert` that accepts two arguments `name` and `size` and returns `true` if the item size is less than or equal the `safeSize`.

   ```js
   const Safe = function (safeSize) {
     // TODO: Your code here
   };

   const safe = new Safe(10);

   safe.insert("passport", 1); // => true
   safe.insert("laptop", 8); // => true
   safe.insert("chair", 20); // => false
   ```

2. Modify `Safe` to have a `storage` attribute that holds the previously inserted items, then modify `insert` to work with the previously inserted items so the more you insert into the safe the less space is left to insert more stuff, in the case that the size exceeds the `safeSize` return `false`.

   ```js
   const safe = new Safe(10);

   safe.insert("passport", 1); // => true
   safe.insert("watch", 1); // => true
   safe.insert("laptop", 8); // => true
   safe.insert("money", 2); // => false
   ```

3. Write a method `remove` that removes the specified item from the `storage` and returns the removed item and if not found return a string `Not Found`, incase there are multiple items with the same name return the first one found.

   ```js
   const safe = new Safe(10);

   safe.insert("watermelon", 7); // => true
   safe.insert("plate", 2); // => true

   safe.remove("money"); // => "Not Found"
   safe.remove("watermelon"); // => {name: "watermelon", "size: 7"}
   safe.remove("watermelon"); // => "Not Found"
   ```

4. Modify `Safe` to have a `passcode` attribute and a `setPassCode` method, that accepts a passcode and saves it in the safe then return `Passcode has been set` and if there is already a passcode return `Reset passcode first`.

   ```js
   const safe = new Safe(10);

   safe.setPassCode("8642"); // => "Passcode has been set"
   safe.setPassCode("7531"); // => "Reset passcode first"
   ```

5. Write a method `resetPassCode` that accepts a passcode argument and resets the passcode if the saved passcode matches the provided one and returns `Passcode has been reset` and if there was no saved passcode return `Set a passcode first` and lastly in the case of providing a passcode that doesn't match the saved one then return `Wrong passcode`.

   ```js
   const safe = new Safe(10);

   safe.resetPassCode("8642"); // => "Set a passcode first"
   safe.setPassCode("8642"); // => "Passcode has been set"
   safe.setPassCode("7531"); // => "Reset passcode first"

   safe.resetPassCode("7531"); // => "Wrong passcode"
   safe.resetPassCode("8642"); // => "PassCode has been reset"
   safe.setPassCode("7531"); // => "Passcode has been set"
   ```

6. Modify `Safe` to have `isOpen` attribute and `openSafe` method, that accepts a passcode and sets `isOpen` to `true` and returns `The safe is open and ready to use` if the passcode provided matches the saved one otherwise return `Wrong passcode`

   ```js
   const safe = new Safe(10);

   safe.openSafe(); // => "The safe is open and ready to use"
   safe.setPassCode("8642"); // => "Passcode has been set"
   safe.openSafe("7531"); // => "Wrong passcode"
   safe.openSafe("8642"); // => "The safe is open and ready to use"
   ```

7. Write a method `closeSafe` that sets `isOpen` to `false` and returns `The safe is closed`

   ```js
   const safe = new Safe(10);

   safe.openSafe(); // => "The safe is open and ready to use"
   safe.closeSafe(); // => "The safe is closed"
   ```

8. Modify `insert` and `remove` to only work if the safe is opened, if the safe is closed then return `Please open the safe first`.

   ```js
   const safe = new Safe(10);

   safe.setPassCode("8642"); // => "Passcode has been set"

   safe.insert("laptop", 8); // => "Please open the safe first"
   safe.remove("laptop"); // => "Please open the safe first"

   safe.openSafe("7531"); // => "Wrong passcode"
   safe.openSafe("8642"); // => "The safe is open and ready to use"

   safe.insert("watermelon", 7); // => true
   safe.remove("watermelon"); // => {name: "watermelon", "size: 7"}

   safe.closeSafe(); // => "The safe is closed"
   safe.insert("watermelon", 7); // => "Please open the safe first"
   ```
  
9. Modify `Safe` to have a method `lockSafe` that will trigger in the case of `x` amount of failed attempts to open the safe, that method will lock the safe and prevent it from opening up and it should return `The Safe is locked` when trying to open it.

   ```js
   const safe = new Safe(10, 2);

   safe.setPassCode("8642"); // => "Passcode has been set"

   safe.openSafe("7531"); // => "Wrong passcode"
   safe.openSafe("9713"); // => "The Safe is locked"
   safe.openSafe("8642"); // => "The Safe is locked"
   ```

10. Modify `Safe` to have `lockDownDuration` in milliseconds (5000 equal to 5 seconds) that will be used in `lockSafe` to lock the safe for that duration and during it the safe can't be opened.

    ```js
    const safe = new Safe(10, 2, 5000);

    safe.setPassCode("8642"); // => "Passcode has been set"

    safe.openSafe("7531"); // => "Wrong passcode"
    safe.openSafe("9713"); // => "The safe is locked"
    safe.openSafe("8642"); // => "The safe is locked"
    // after 5 seconds have passed the safe shouldn't be locked anymore
    safe.openSafe("9713"); // => "Wrong passcode"
    safe.openSafe("8642"); // => "The safe is open and ready to use"
    ```

     <details>
      <summary>
        Click here for HINT
      </summary>
      Read About `setTimeout`
    </details>

### Extra Practice

1. Write a function `Pie` that accepts two arguments `name` and `ingredients` and returns an object representing the pie.

   ```js
   const Pie = function (name, ingredients) {
     // TODO: Your code here
   };

   const applePie = Pie("Apple Pie", ["Apples", "Sugar", "Cinnamon"]);
   applePie; // => { name: "Apple Pie", ingredients: ["Apples", "Sugar", "Cinnamon"] }

   const pecanPie = Pie("Pecan Pie", ["Pecans", "Brown Sugar", "Corn Syrup"]);

   pecanPie; // => { name: "Pecan Pie", ingredients: ["Pecans", "Brown Sugar", "Corn Syrup"] }
   ```

2. Write a method `bake` that accepts one argument `duration`, modify `Pie` to have a a baking duration attribute that represent time in seconds, if the pie is baked for more than the specified duration by 10 seconds then the `bake` method will return a string `Burnt pieName` and if it was under by 10 seconds then return `Under cooked pieName` otherwise return a string `Baked pieName`, make sure to modify the pie name to be equal to the return value after baking.

   ```js
   const bake = function (duration) {
     // TODO: Your code here
   };

   // the baking time for the pie is 30 seconds
   const applePie = Pie("Apple Pie", ["Apples", "Sugar", "Cinnamon"], 30);

   applePie.bake(20); // => "Under cooked Apple Pie"
   applePie.bake(40); // => "Burnt Apple Pie"
   applePie.bake(30); // => "Baked Apple Pie"
   applePie.bake(35); // => "Baked Apple Pie"
   applePie.bake(25); // => "Baked Apple Pie"
   ```

3. Write a method `slicePie` that slices backed pies in half and returns the amount of slices, if it is used on an unbaked pie then return a string `Bake the pie first`.

   ```js
   const slicePie = function () {
     // TODO: Your code here
   };

   const applePie = Pie("Apple Pie", ["Apples", "Sugar", "Cinnamon"], 30);

   applePie.slicePie(); // => "Bake the pie first"

   applePie.bake(30); // => "Baked Apple Pie"
   applePie.slicePie(); // => "2 slices"
   applePie.slicePie(); // => "4 slices"
   applePie.slicePie(); // => "6 slices"
   ```

4. Write a method `checkIngredients` that accepts an array of ingredients and checks wither all of them are used in the pie, and returns `true` if all the ingredients are present in the pie otherwise return `false`, the method should only work before baking the pie if it is used on a baked pie return `Already baked`

   ```js
   const checkIngredients = function (ingredients) {
     // TODO: Your code here
   };

   const applePie = Pie("Apple Pie", ["Apples", "Sugar", "Cinnamon"], 30);

   applePie.checkIngredients(["Cinnamon", "Apples"]); // => true
   applePie.checkIngredients(["Blueberries", "Sugar"]); // => false

   applePie.bake(30); // => "Baked Apple Pie"

   applePie.checkIngredients(["Cinnamon", "Apples"]); // => "Already baked"
   applePie.checkIngredients(["Blueberries", "Sugar"]); // => "Already baked"
   ```

5. Write a method `addTopping` that accepts an argument `topping` and modifies the name of the pie to be `pieName with toppingName` then returns the new name of the pie and it should work only one baked pies and if used on an unbaked one then return `Please bake the pie first`, also modify the method `bake` to only work once on each pie and if used on the same baked pie it should return `Already baked`.

   ```js
   const addTopping = function (topping) {
     // TODO: Your code here
   };

   const applePie = Pie("Apple Pie", ["Apples", "Sugar", "Cinnamon"], 30);

   applePie.bake(30); // => "Baked Apple Pie"
   applePie.bake(30); // => "Already baked"

   applePie.addTopping("Ice Cream"); // => "Baked Apple Pie with Ice Cream"
   ```

6. Modify the method `bake` to remove the bake duration and to log each second that passes till it reaches the duration time for the recipe then changes the name to `Baked pieName` and logs the name after changing it.

   ```js
   const applePie = Pie("Apple Pie", ["Apples", "Sugar", "Cinnamon"], 30);

   applePie.bake();
   // 1 second have passed
   // 2 seconds have passed
   // 3 seconds have passed
   // 4 seconds have passed
   // .....
   // 29 seconds have passed

   // after the time is over (30 seconds) it will log the new name of the pie
   // 30 seconds have passed
   // Baked Apple Pie
   ```

   <details>
     <summary>
       Click here for HINT
     </summary>
     Read About `setInterval`
   </details>

7. Write a function `stopBaking` that stops the `bake` method and if there is more than 10 seconds left for the pie to be ready log `Undercooked pieName` otherwise log `Baked pieName`.

   ```js
   const applePie = Pie("Apple Pie", ["Apples", "Sugar", "Cinnamon"], 30);

   applePie.bake();
   // after 10 seconds have passed
   applePie.stopBaking();
   // Undercooked Apple Pie

   const pecanPie = Pie(
     "Pecan Pie",
     ["Pecans", "Brown Sugar", "Corn Syrup"],
     30
   );
   pecanPie.bake();
   // after 25 seconds have passed
   pecanPie.stopBaking();
   // Baked Pecan Pie
   ```

   <details>
     <summary>
       Click here for HINT
     </summary>
     Read About `clearInterval`
   </details>
