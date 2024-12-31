# Objects In JavaScript

## High Level Goals

By the end of this lesson, you will be familiar with the following:

- Defining an object
- Accessing values
- Assigning values
- Factory functions

## Objects

### What are Objects

An object is an unordered collection that consists of paired keys and values. There are no restrictions on data types when creating an object, but usually, it is preferred to hold values that correspond to what the value of the key should be.

Defining an object (with examples):

```js
const object = {}; // => empty object

// in between the curly brackets `{}` add comma-separated key and value pairs where the key and the value are separated by a colon `:`
const name = { first: "John", last: "Doe" };

const numbers = { odd: [1, 3, 5], even: [2, 4, 6] };

const someObjectValues = {
  number: 100,
  string: "Hello World",
  array: [1, 2],
  boolean: true,
  object: { a: 1 },
  square: function (number) {
    return number * number;
  },
};

// it is possible to use other variables inside the object
const firstName = "John";
const lastName = "Doe";

const fullName = { first: firstName, last: lastName };
```

### Accessing and Assigning values

In order to access a value in the object, we need to reference the object and its key name. There are two ways we can do that, dot notations and bracket notations.

Here is an example

```js
const name = { first: "John", last: "Doe" };

// this is how a dot notation looks like
name.first; // => "John"
name.last; // => "Doe"

// this is how a bracket notation looks like
name["first"]; // => "John"
name["last"]; // => "Doe"

// bracket notations can be used with variables while dot notations can't be used with variables
const keyName = "first";

name[keyName]; // => "John"
name.keyName; // => undefined

// accessing nested objects
const nestedObjects = { name: { first: "John", last: "Doe" } };
nestedObjects.name.first; // => "John"
nestedObjects.name.last; // => "Doe"

// to assign new values or update existing ones, refer to the key and then use
// the assignment operator to update or add a new key and value pair
const object = { firstKey: 10, secondKey: 20 };

object.firstKey = 100;
object; // => {firstKey: 100, secondKey: 20}
object["thirdKey"] = 30;
object.fourthKey = 40;
object; // => {firstKey: 100, secondKey: 20, thirdKey: 30, fourthKey: 40}
```

### Factory functions

In JavaScript, a factory function is a function that returns an object without using the keyword `new`.

Example on factory functions:

```js
// people is an array that holds objects that represent a person
const people = [];

// imagine if we want to fill the people's array with twenty objects, it would be a bit tedious to
// create so many objects in this way to add to the array
const personOne = { name: "John", age: 23 };
const personTwo = { name: "Jane", age: 26 };

people.push(personOne, personTwo);
people; // => [{name:"John", age:23}, {name:"Jane", age:26}]

// so we could use a function to create the objects for us instead
const createPerson = function (name, age) {
  return { name: name, age: age };
};

personThree = createPerson("Mark", 19);
personFour = createPerson("Marry", 20);
people.push(personThree, personFour);
```

### Pulse Check

1. Define the following objects.

   - Define an object `person` containing three attributes: `name`, `age`, `gender`.

   - Define an object `movie`containing three attributes: `name`, `length`, `genre`.

   - Define an object `favoriteFood` containing an array of your favorite foods.

   - Define an object `store` containing two attributes, `name` and `address`. Address is an object with two attributes, `buildingNumber` and `street`.

2. Access the following values.

   - Access the value of the key `Mars` in the following objects:

   ```js
   // a- using a dot notation
   const orderedSolarSystem = {
     Mercery: "first",
     Venus: "second",
     Earth: "third",
     Mars: "fourth",
   };
   // b- using a bracket notation
   const unorderedSolarSystem = {
     Mars: "fourth",
     Earth: "third",
     Mercery: "first",
     Venus: "second",
   };
   ```

   - Access the value of the key `koala` in the following object:

   ```js
   const animalDiet = {
     mammals: {
       cat: "carnivore",
       dog: "carnivore",
       koala: "herbivore",
     },
     fish: {
       shark: "carnivore",
     },
   };
   ```

3. Assign the following values to the corresponding object.

   - Add the math grade (80) to the student using a dot notation.
   - Change the english grade to a 90 using a dot notation.
   - Add an attribute average with the average of the score of all three grades using a dot notation.

   ```js
   const studentOne = {
     englishGrade: 80,
     scienceGrade: 90,
   };
   ```

   - Add the math grade (80) to the student using a bracket notation.
   - Change the english grade to an 90 using a bracket notation.
   - Add an attribute average with the average of the score of all three grades using a bracket notation.

   ```js
   const studentTwo = {
     englishGrade: 80,
     scienceGrade: 90,
   };
   ```

   - Assign the following variables as a key-value pair to the object. Make sure to use the name of the variables.

   ```js
   const objectKey = "key";
   const ObjectValue = "value";

   const object = {};
   ```

### Practice

1. Figure out the syntax errors in the following, and fix them.

   ```js
   const person = (name: john, age:20)

   const car = {brand "Toyota", model: 2020}

   const employee ={name: "Jane", position: developer}
   ```

2. Check the following objects and solve the requirements.

   - Access the `age` property.
   - Modify the person's age to be 23 years old.
   - Add a property called `work` with the value of an object with two keys, `position` and `salary`.

   ```js
   const person = {
     firstName: "John",
     lastName: "Doe",
     age: 24,
   };
   ```

   - Access the first name property of both employees.
   - Add an employee object with your name and the position of full-stack developer.

   ```js
   const employees = [
     {
       id: 1,
       name: {
         first: "John",
         last: "Doe",
       },
       position: "Designer",
     },
     {
       id: 2,
       name: {
         first: "Jane",
         last: "Doe",
       },
       position: "Engineer",
     },
   ];
   ```

   - Access the model value of both cars.
   - Change the prius model from 2019 to 2020.
   - Add a new car of your choice.
   - Add a property `isAutomatic` for all three cars.

   ```js
   const cars = {
     toyota: {
       name: "prius",
       model: 2019,
     },
     nissan: {
       name: "leaf",
       model: 2020,
     },
   };
   ```

3. Write a factory function `createUser` that accepts two string arguments, `firstName` and `lastName`, returning an object representing the user.

   ```js
   const createUser = function (firstName, lastName) {
     // TODO: Your code here
   };

   createUser("John", "Doe"); // => {firstName: "John", lastName: "Doe"}
   createUser("Peter", "Brown"); // => {firstName: "Peter", lastName: "Brown"}
   ```

4. Write a factory function `createCar` that accepts three string arguments, `brand`, `name`, and `color`, returning an object representing the car.

   ```js
   const createCar = function (brand, name, color) {
     // TODO: Your code here
   };

   createCar("Toyota", "Prius", "Black"); // => {brand: "Toyota", name: "Prius", color: "Black"}
   createCar("Audi", "A1", "Blue"); // => {brand: "Audi", name: "A1", color: "Blue"}
   ```

5. Write a function `getFullName` that accepts an object representing a person and returns that person's full name in a string.

   ```js
   const getFullName = function (person) {
     // TODO: Your code here
   };

   getFullName({ first: "Elon", middle: "Reeve", last: "Musk" }); // => "Elon Reeve Musk"
   getFullName({ first: "John", middle: "Mark", last: "Doe" }); // => "John Mark Doe"
   ```

6. Write a function `olderThan` that accepts two objects, `personOne` and `personTwo`, and returns a string that represent who is older than the other.

   ```js
   const olderThan = function (personOne, personTwo) {
     // TODO: Your code here
   };

   olderThan({ name: "John", age: 23 }, { name: "Jane", age: 26 }); // => "Jane is older than John"
   olderThan({ name: "Mark", age: 30 }, { name: "Smith", age: 25 }); // => "Mark is older than Smith"
   olderThan({ name: "Marry", age: 20 }, { name: "Sarah", age: 20 }); // => "Marry is as old as Sarah"
   ```

7. Write a function `isPropertyOf` that accepts a string and an object and returns `true` if the string is a property of the object. Return `false` if it isn't.

   ```js
   const isPropertyOf = function (string, object) {
     // TODO: Your code here
   };

   isPropertyOf("hello", { hello: "world" }); // => true
   isPropertyOf("world", { hello: "world" }); // => false
   ```

8. Write a function `numberOfKeys` that accepts an object and returns the number of keys present in the object.

   ```js
   const numberOfKeys = function (object) {
     // TODO: Your code here
   };

   numberOfKeys({ name: "James", age: 27 }); // => 2
   numberOfKeys({ fruit: "orange", vegetable: "broccoli", animal: "cat" }); // => 3
   ```

   HINT: search for `Object.keys()` on MDN.

9. Write a function `valuesToString` that accepts an object and returns a string of all the values from the object separated by an empty space.

   ```js
   const valuesToString = function (object) {
     // TODO: Your code here
   };

   valuesToString({ name: "James", age: 27 }); // => "James 27"
   valuesToString({ fruit: "apple", vegetable: "asparagus", animal: "dog" }); // => "apple asparagus dog"
   ```

   HINT: search for `Object.values()` on MDN.

10. Write a function `keyInObject` that accepts two arguments, `object` and `key`, and checks if the key is present within the object. Return `true` if the key is present and `false` if it is absent.

    ```js
    const keyInObject = function (object, key) {
      // TODO: Your code here
    };

    keyInObject(
      { order: "chicken sandwich", orderId: 0, quantity: 1 },
      "orderId"
    ); // => true
    keyInObject(
      { order: "hamburger with fries", orderId: 1, quantity: 2 },
      "name"
    ); // => false
    ```

    HINT: search for `.hasOwnProperty()` on MDN.

### Extra Practice

1. Check the following object and solve the requirements.

   - Access the value of Sarah's children and the value of Samuel's children.
   - Add a child for Samuel named Sam that has two children Marry and Gwen.
   - Delete the `children` property from the people who don't have children.

   ```js
   // HINT: read about the delete operator
   const family = {
     name: "John",
     children: [
       {
         name: "Bill",
         children: [
           {
             name: "Mark",
             children: [],
           },
           {
             name: "Sarah",
             children: [
               {
                 name: "Smith",
                 children: [],
               },
               {
                 name: "Stan",
                 children: [],
               },
             ],
           },
           {
             name: "Samuel",
             children: [],
           },
         ],
       },
       {
         name: "Jane",
         children: [],
       },
     ],
   };
   ```

2. Write a factory function `createIceCream` that accepts Three arguments, `coneType`, `flavour`, and `topping`, and returns an object representing the ice-cream.

   ```js
   const createIceCream = function (coneType, iceCreamFlavour, topping) {
     // TODO: Your code here
   };

   createIceCream("wafer cone", "chocolate"); // => {coneType: "wafer cone" flavour: "chocolate", topping: "none"}
   createIceCream("waffle cone", "vanilla", "chocolate syrup"); // => {coneType: "waffle cone", flavour: "vanilla", topping: "chocolate syrup"}
   createIceCream("sugar cone", "strawberry", "cherry"); // => {coneType: "sugar cone", flavour: "strawberry", topping: "cherry"}
   ```

3. Try the following code and explain the results

   ```js
   const employeeOne = {
     id: 0,
     name: "John",
     position: "",
   };

   const employeeTwo = {
     id: 1,
     name: "Jane",
     position: "Developer",
   };

   if (employeeOne.id) {
     console.log(employeeOne.name);
   }

   if (employeeTwo.id) {
     console.log(employeeOne.name);
   }

   if (employeeOne.position) {
     console.log(employeeOne.name);
   }

   if (employeeTwo.position) {
     console.log(employeeOne.name);
   }

   if (employeeOne.salary) {
     console.log(employeeOne.name);
   }
   ```

4. Write a function `isValidUser` that accepts an object representing login information and returns `true` if the user is valid otherwise return `false`. Read the comments for more information.

   ```js
   // things to validate:
   // 1- length of the email is greater than or equal to 6
   // 2- length of the password is greater than or equal to 8
   // 3- email contains `@` and `.com`
   // 4- the user must be in the users object
   // 5- both of the passwords match
   // 6- when you compare information make sure to reference the users object and access the value form there
   const users = {
     mrpotato: {
       email: "mr.potato@gmail.com",
       password: "LonelyPotato",
     },
     thewiseman: {
       email: "wiseMan9999@gmail.com",
       password: "12345678",
     },
   };

   const isValidUser = function (loginInfo) {
     // TODO: Your code here
   };

   isValidUser({
     username: "MrPotato",
     email: "mr.potato@gmail.com",
     password: "LonelyPotato",
   }); // => true

   isValidUser({
     username: "MrPotato",
     email: "mr.potato@gmail.com",
     password: "Lonely",
   }); // => false

   isValidUser({
     username: "MrPotato",
     email: "mr.potato.gmail.com",
     password: "LonelyPotato",
   }); // => false
   ```

5. Write a function `compareKeys` that accepts two objects and returns `true` if the key names and their order match. Return `false if they don't`.

   ```js
   const compareKeys = function (objectOne, objectTwo) {
     // TODO: Your code here
   };

   compareKeys({ name: "James", age: 27 }, { name: "Sam", age: 24 }); // => true
   compareKeys({ name: "John", age: 23 }, { word: "Hello", place: "New York" }); // => false
   ```
