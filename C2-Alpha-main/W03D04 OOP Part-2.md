# ES6 Classes

## High Level Goals

By the end of this lesson, you will be familiar with the following:

- Classes
- Inheritance using extends

## OOP Using ES6

### Classes

Classes are used as a template for creating objects, Classes are defined using the keyword `class` and they are mainly syntactical sugar added to make the function seem to have a class-like semantic while in reality it is still built on prototypes.

There are two ways to create classes the first is `class declaration` which is commonly used and `class expression`, we will use `class declaration` as our main way of creating classes.

An example on creating a class using `class`

```js
// by using `class` it is possible to create a Class
class Employee {}
// when creating an instance of the Class, it is a must to add the `new` keyword otherwise the following error will be thrown
// Uncaught TypeError: Class constructor Employee cannot be invoked without 'new'
const emp1 = Employee();

const emp1 = new Employee();
// Employee instance
emp1; // => Employee {}
```

An example on the constructor method

```js
//
class Employee {
  // constructor is a special method used for initializing objects created with the keyword `class`
  // the constructor parameters are the arguments passed when creating the instance
  constructor(name, salary) {
    // set the attributes using keyword `this`
    this.name = name;
    this.salary = salary;
  }
}

const emp2 = new Employee("John",  1000);
emp2.name; // => "John"
```

An example on prototype methods

```js
class Employee {
  constructor(name, salary) {
    this.name = name;
    this.salary = salary;
  }

  // add the method name directly without having to type `function` before it
  getName() {
    return `name: ${this.name}`;
  }
}

const emp3 = new Employee("John", 1000);

emp3.getName(); // => name: John
```

### Inheritance Using Extends

Inheritance which is also known as sub classing can be done in ES6 by using the keyword `extends`.

Example on inheritance by using `extends`

```js
class Employee {
  constructor(name, salary) {
    this.name = name;
    this.salary = salary;
  }

  getName() {
    return `name: ${this.name}`;
  }
}

class Developer extends Employee {
  constructor(name, salary, position) {
    // super refers to the Employee constructor
    super(name, salary);
    this.position = position;
  }

  getPosition() {
    return `position: ${this.position}`;
  }
}

const developer = new Developer("John", 600, "Junior Developer");

developer.getName(); // => "name: John"
developer.getPosition(); // => "position: Junior Developer"
```

### Practice

1. Refactor your solution for the practice questions from lesson eleven to use classes.

### Extra Practice

1. Refactor your solution for the extra practice questions from lesson eleven to use classes.
