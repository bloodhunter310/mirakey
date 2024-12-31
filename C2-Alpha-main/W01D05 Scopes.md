# Scopes In JavaScript

## High Level Goals

By the end of this lesson, you will be familiar with the following:

- Defining a scope
- Global scope
- Local scope
- Closures

## Scopes

### What Are Scopes

Scopes represent the accessibility of `variables`, `functions`, etc. in the code depending on the location of these things.This means that depending on the scope, a variable might be visible in one region of the code but not the in a different region.

There are two types of scopes in JavaScript, `local scope` and `global scope`. Local scope refers to the inside of the current scope, an example of that would be the inside of a function's code block where everything inside is considered the local scope when executing the function meaning that all variables defined there will be accessible, and the global scope will be the scope were the function is defined in.

When it comes to accessibility, local scopes can access global scopes, but not the other way around. This means that when trying to access a variable, it only goes outwards from the local scope to other global scopes.

Let's explore the global scope.

```js
// global Scope
// an example of a global variable used in the local scope of a function

const person = "John";

const greet = function () {
  // start of local Scope
  // the variable person doesn't exist in the local scope of the function which will result in
  // the function looking for the variable in the outer scope that is considered global to it
  return "Hello " + person;
  // end of local Scope
};

greet(); // => "Hello John"
person; // => "John"

// an example to show that it is possible to reassign the value of a global variable in the local scope
let person = "Mark";

const updatePerson = function (newName) {
  //Start of local Scope
  person = newName;
  //End of local Scope
  return person;
};

updatePerson("Jane"); // => "Jane"
person; // => "Jane"
```

Let's explore the local scope.

```js
// an example to show how the code is encapsulated within the function's scope and can't be accessed outside

const greeting = function (fName) {
  //Start of local Scope
  // a local scope variable is accessible inside the same scope but not from outside
  let firstName = fName;
  return "Hello " + firstName;
  //End of local Scope
};

greeting("Mark"); // => "Hello Mark"
firstName; // =>  Uncaught ReferenceError: firstName is not defined
```

### Block Statements

Any block statement that has its own code block such as `if`, `else if`, and `else` doesn't create a local scope by default, but by using `let` and `const` to define variable inside it makes it act like a local scope. Contrary to the old way of declaring variables with the `var` keyword that can be accessed from outside the block statement.

```js
const example1 = function () {
  // local scope

  if (true) {
    // block scope
    // these variables are only accessible inside the code block
    const gender = "John";
    let age = 24;
  }

  console.log(gender); // ReferenceError: gender is not defined
  console.log(age); // ReferenceError: gender is not age
};

example1();

const example2 = function () {
  // local scope
  if (true) {
    // block scope
    // the variable can be accessed outside the block scope since it was defined using `var`
    var isActive = true;
  }

  console.log(isActive); // true
};

example2();
```

### Closures

A closure is the combination of a function bundled with references to its surrounding lexical environment. A closure gives you access to an outer function’s scope from an inner function.

Closures are used to persist data without having to define variables in the global scope, and they are good to keep some variables private.

```js
// an example on persisting data without using closures (using global variables)
let lightSwitch = "OFF";

const toggleLight = function () {
  if (lightSwitch === "OFF") {
    lightSwitch = "ON";
    return "the light is " + lightSwitch;
  } else {
    lightSwitch = "OFF";
    return "the light is " + lightSwitch;
  }
};
// above we have a function that toggles a global variable ON and OFF
//what if we had multiple functions that are controlling other light switches?
//they all would be using the same variable and that would result in a mess, so to solve that we could use closures

const toggle = function () {
  let lightSwitch = "OFF";

  // this anonymous function is a closure function that has access to its own closure variable
  return function () {
    if (lightSwitch === "OFF") {
      lightSwitch = "ON";
      return "the light is " + lightSwitch;
    } else {
      lightSwitch = "OFF";
      return "the light is " + lightSwitch;
    }
  };
};

// the variable will be equal to the return value of toggle so it will be equal to the closure function
const toggleLight1 = toggle();
// we need a second invocation to be able to invoke the closure function
toggleLight1(); // => 'the light is ON'
toggleLight1(); // => 'the light is OFF'
toggleLight1(); // => 'the light is ON'
// we can create another variable to control another light
const toggleLight2 = toggle();
toggleLight2(); // => 'the light is ON'
toggleLight2(); // => 'the light is OFF'
toggleLight1(); // => 'the light is OFF'
// now we have persisted data without using a global variable
```

### Pulse Check

1. Create a global variable `myFavoriteFood` and return its value in the function's local scope.

   ```js
   // make sure that the variable is in the global scope
   const favoriteFood = function () {
     // TODO: Your code here
   };

   favoriteFood(); // => the value of `myFavoriteFood` variable
   ```

2. Create a function `updateFavoriteFood` that updates the value of `myFavoriteFood`

   ```js
   const updateFavoriteFood = function (newValue) {
     // TODO: Your code here
   };

   updateFavoriteFood("Pizza");
   favoriteFood(); // => "Pizza"
   ```

3. Use the following closure function to create two separate counters

   ```js
   const createCounter = function () {
     let counter = 0;

     // this anonymous function is a closure function that has access to its own closure variable
     return function () {
       return ++counter;
     };
   };
   ```

4. Modify `createCounter` to take a parameter that represents the starting point for the counter

   ```js
   // instead of counting from zero it will take count from the value provided
   const createCounter = function (start) {
     // TODO: Your code here
   };
   ```

### Practice

1. Predict the value of the following variables and explain why.

   ```js
   let age = 25;
   if (true) {
     age = 30;
   }
   age; // ?

   const myName = "John";
   if (true) {
     const myName = "Jane";
   }
   myName; // ?
   ```

2. Predict the value of the following function invocations.

   ```js
   let number = 10;
   const func1 = function () {
     let number = 15;

     if (true) {
       let number = 24;
     }

     return number;
   };

   func1(); // ?

   const func2 = function (age) {
     age = 10;
     if (true) {
       let age = 24;
       age = 20;
     }

     return age;
   };

   func2(26); // ?
   ```

3. Write a function `countDown` that returns a number representing a count down value. With each invocation the number should be lower by one and at zero it will no longer decrement and instead it will return `"count down is over"`.

   ```js
   const countDown = function () {
     // TODO: Your code here
   };

   countDown(); // => 4
   countDown(); // => 3
   countDown(); // => 2
   countDown(); // => 1
   countDown(); // => 0
   countDown(); // => "count down is over"
   ```

4. Write a function `countUp` that should do the opposite of `countDown`. With every invocation the count value should be incremented by one.

   ```js
   const countUp = function () {
     // TODO: Your code here
   };

   countUp(); // => 4
   countUp(); // => 5
   countUp(); // => 6
   countUp(); // => 7
   countUp(); // => 8
   ```

5. Write a function `resetCount` that accepts a number argument `start` and updates the count variable to equal the starting value and return a string implying that.

   ```js
   const resetCount = function (start) {
     // TODO: Your code here
   };

   resetCount(0); // => "the count has been reset"
   countUp(); // => 1
   resetCount(10); // => "the count has been reset"
   countUp(); // => 11
   ```

6. Write a function `addToList` that accepts a string argument `toDo` and returns the current list as a string. Every time we invoke the function it should return the old toDo item plus the new one.

   ```js
   const addToList = function (toDo) {
     // TODO: Your code here
   };

   addToList("Eat"); // => 'Eat'
   addToList("Play"); // => 'Eat Play'
   addToList("Sleep"); // => 'Eat Play Sleep'
   addToList("repeat"); // => 'Eat Play Sleep repeat'
   ```

7. Write a function `createToDoList` that works similarly to `addToList` function but instead of a global variable use a closure variable.

   ```js
   const createToDoList = function () {
     // TODO: Your code here
   };

   const toDoListOne = createToDoList();
   toDoListOne("Eat"); // => 'Eat'
   toDoListOne("Play"); // => 'Eat Play'
   toDoListOne("Sleep"); // => 'Eat Play Sleep'
   toDoListOne("repeat"); // => 'Eat Play Sleep repeat'
   ```

8. Write a function `deposit` that accepts a number argument `amount` and returns the current account balance after depositing the amount.

   ```js
   const deposit = function (amount) {
     // TODO: Your code here
   };

   deposit(100); // => 100
   deposit(50); // => 150
   ```

9. Write a function `withdraw` that accepts a number argument `amount` and returns the current account balance after withdrawing the amount.

   ```js
   const withdraw = function (amount) {
     // TODO: Your code here
   };

   deposit(100); // => 100
   deposit(50); // => 150
   withdraw(70); // => 80
   deposit(50); // => 130
   withdraw(100); // => 30
   withdraw(100); // => "insufficient funds, current balance: 30"
   ```

10. Write a closure function `createAccount` that accepts a number argument `initialValue` that represents the starting value of the account balance and return a closure function with two parameters, `transactionType` and `amount` that deposit or withdraw from the account balance depending on the `transactionType`and returns the total balance amount. Make sure to prevent transactions that withdraw more than the total balance.

    ```js
    const createAccount = function (initialValue) {
      // TODO: Your code here
    };

    const accountOne = createAccount(0);
    accountOne("withdraw", 10); // => "insufficient funds, current balance: 0"
    accountOne("deposit", 50); // => 50
    accountOne("deposit", 70); // => 120
    accountOne("withdraw", 10); // => 110

    const accountTwo = createAccount(500);
    accountTwo("withdraw", 100); // => 400
    accountTwo("withdraw", 100); // => 300
    accountTwo("deposit", 50); // => 350
    accountTwo("withdraw", 500); // => "insufficient funds, current balance: 350"
    ```

### Extra Practice

1. Write a function `minMax` that accepts a number argument `number` and returns a string representing the maximum and the minimum numbers. Read the comments for more information.

   ```js
   // every time the function is called it must check if the passed argument is the maximum number, minimum number, or
   // both, and preserve the result for later invocations
   const minMax = function (number) {
     // TODO: Your code here
   };

   minMax(5); // => "the maximum number is: 5 and the minimum number is 5"
   minMax(2); // => "the maximum number is: 5 and the minimum number is 2"
   minMax(3); // => "the maximum number is: 5 and the minimum number is 2"
   minMax(7); // => "the maximum number is: 7 and the minimum number is 2"
   minMax(0); // => "the maximum number is: 7 and the minimum number is 0"
   ```

   HINT search for NEGATIVE_INFINITY and POSITIVE_INFINITY on [MDN](https://developer.mozilla.org/en-US/).

2. Modify the `rockPaperScissors` function from the previous lesson to save the score of how many times the user has won and how many the user has lost. Return the score with every invocation.

   ```js
   // use your previous solution for `randomMove`
   const randomMove = function () {
     // TODO: Your code here
   };

   const rockPaperScissors = function (move) {
     // TODO: Your code here
   };

   rockPaperScissors("rock"); // => "Won: 1, Lost:0"
   rockPaperScissors("rock"); // => "Won: 1, Lost:1"
   rockPaperScissors("paper"); // => "Won: 1, Lost:2"
   ```

3. Modify the `rockPaperScissors` function to have a score limit such as winning five times then reset the score back to zero.

   ```js
   // lets assume that the score limit is set to three
   rockPaperScissors("rock"); // => "Won: 2, Lost:2"
   rockPaperScissors("rock"); // => "Won: 2, Lost:3"
   rockPaperScissors("rock"); // => "Won: 1, Lost:0"
   ```

4. Modify the `rockPaperScissors` function to have an optional second boolean parameter `reset` that when true will reset the game score back to zero.

   ```js
   const rockPaperScissors = function (move, reset) {
     // TODO: Your code here
   };

   rockPaperScissors("rock"); // => "Won: 1, Lost:0"
   rockPaperScissors("", true); // => "the game has been reset"
   rockPaperScissors("scissors"); // => "Won: 0, Lost:1"
   ```

5. Modify the `rockPaperScissors` function to keep track of the last winner and modify the `randomMove` function to have a 25% chance of picking the same move if the user have lost the previous round, otherwise it picks a random move.

   ```js
   rockPaperScissors("rock"); // => "Won: 0, Lost:1"
   // lets assume that the same random move was picked because of the 25% chance
   rockPaperScissors("rock"); // => "Won: 0, Lost:2"
   rockPaperScissors("rock"); // => "Won: 1, Lost:0"
   ```
