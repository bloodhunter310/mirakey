# TypeScript (TS)

## High Level Goals

By the end of this lesson, you will be familiar with the following:

- TypeScript
- Data Types in TS

## TypeScript

### What Is TypeScript

TypeScript is a superset of JavaScript developed by Microsoft meaning that it has all the feature of JavaScript plus some extra added features and syntax. It can be used with many different technologies like React, Angular, Nodejs and it gets compiled into JavaScript.

To learn more about TypeScript and test it out checkout the TS [documentation](https://www.typescriptlang.org/) and the TS [playground](https://www.typescriptlang.org/play).

### Advantages Of TypeScript

One of the advantages of using TypeScript is the ability add types to JavaScript which would reduce the amount of errors. The IDE would catch the potential errors or unexpected behaviors before the run time, which makes it way easier to develop applications since it gives a lesser margin for error.

### TypeScript Types

Here are some of the types used in TS:

- Any
- String
- Number
- Boolean
- Array
- Void
- Null

### Using TypeScript

In this lesson we will not be focusing on how to compile TS into JS but more into it's syntax, since it will be most likely used with other libraries or frameworks the compiling would be handled by the used technology.

Here are some examples on TS Syntax:

```ts
// to add a type to a variable all is needed to do is add a colon (:) after the variable name followed by the type

// declaring a variable with the type of number
let yourAge: number = 10;

// typescript will give a warning similar to this: [typescript] Type 'string' is not assignable to type 'number'.
yourAge = "ten";

// TS also gives default values depending on the first initial value, but it is a good practice to always declare variable with explicit types as shown in the example above
let myAge = 10;
// [typescript] Type 'string' is not assignable to type 'number'.
myAge - "ten";
```

Examples on different types:

```ts
let quantity: number;
quantity = 20;

const age: number = 10;

const myString: string = "this is a string";

const isActive: boolean = false;

const fruits: string[] = ["apple", "banana"];
// Argument of type 'number' is not assignable to parameter of type 'string'.
fruits.push(3);
// gives the same result as above
const cars: Array<string> = ["Mazda", "Toyota"];

// interfaces are good when dealing with object since we can strictly type check the object properties
interface Car {
  year: number;
  model: string;
  price: number;
}

// declaring a new variable using the Car interface as the type
// since the type is an interface then it must be followed. All the properties should only be present in the object and have the correct type
let newCar: Car = {
  year: 2020,
  model: "Some model",
  price: 2000,
};
```

Examples on functions in TS:

```ts
// we can add types for the parameters and also for the function itself
const greeting = (name: string, age: number): string => {
  return `Hello i am ${name} and i am ${age} years old`;
};

let count: number = 10;
// void type is used when the function doesn't have a return or returns `undefined`
const updateCounter = (): void => {
  count++;
};
```

Example on custom types:

```ts
// classes can be used to create custom types to be used in the application
class Employee {
    firstName: String;
    lastName: String;
    salary: Number;

    constructor(firstName: String, lastName: String, salary: Number) {
      this.firstName = firstName;
      this.lastName = lastName;
      this.salary = salary;
    }

    showName(): String {
      return this.firstName + ' ' + this.lastName;
    }

    showSalary(): Number {
      return this.salary;
    }
  }

  // emp1 is type Employee which means it must be an instance of Employee 
  const emp1: Employee = new Employee("John","Doe", 700);

  console.log(emp1.showName());
  console.log(emp1.showSalary());
```
