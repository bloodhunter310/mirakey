# MongoDB and Mongoose

## High Level Goals

By the end of this lesson, you will be familiar with the following:

- Databases
- Advantages of Databases
- MongoDB
- Mongoose
- Mongoose Schema
- Mongoose Model

## Database

A database is an organized collection of information that is built using various design and modeling techniques. Databases are used to save and persist data in our applications as well as prevent data loss in case of server crashes. There are many types of databases that are categorized according to the database models that they support.

Databases are an important part of an application and are usually the starting point of an application. Since the data in the database is representing the inputs and outputs, it makes it a crucial part of the application.

A DBMS (Database Management System) is used to enable the user to interact with the database. Some examples of a DBMS would be: MySQL, PostgreSQL, MongoDB, Oracle, Microsoft Access, and SQL Server. We will be learning MySQL and MongoDB in the next lessons.

### Advantages of Databases

A database has many great advantages such as:

- Great for data management
- Great for analyzing the data
- Provides easy access to the database by multiple users
- Fast queries
- Flexible
- Persisting data
- Less room for error when handling the data

## MongoDB

MongoDb is a document-based database that stores data in a JSON-like document which makes it easy to deal with.

### MongoDB installation

Download MongoDB from this [link](https://www.mongodb.com/try/download/community) and run the installer, continue the installation process and make sure to include MongoDB Compass.

### MongoDB Compass

MongoDB Compass is a graphical user interface (GUI) that is used to interact with the database and analyze the data.

## Mongoose

Mongoose is an NPM package used to model application data, it is used for writing schemas, business logic, and validation. Since it is an NPM package, it can be installed by using `npm i mongoose`.

### Connecting Mongoose

Mongoose can be connected to the database by using the `connect` method. It takes the Database URI as the first parameter, an example of a DB URI would be: `mongodb://user:password@host:port/database`. This connection string can be broken down into a few different parts:

- `mongodb://`: a required prefix when creating connection strings for mongodb
- `user`: the name of the database username
- `password`: the password for the database
- `host`: the URL for the database, it would be `localhost` if the database is ran locally
- `port`: the mongoDB database port `27017` by default
- `database`: the name of the database

db.js

```js
const mongoose = require("mongoose");

const options = {
  useNewUrlParser: true,
  useCreateIndex: true,
  useUnifiedTopology: true,
};

// connecting mongoose
mongoose.connect("mongodb://localhost:27017/DB_Name", options).then(
  () => {
    console.log("DB Ready To Use");
  },
  (err) => {
    console.log(err);
  }
);
```

app.js

```js
const express = require("express");
// require the file to execute it
const db = require("./db");

const app = express();

const port = 3000;
app.listen(port, () => {
  console.log(`Example app listening at http://localhost:${port}`);
});
```

### Mongoose schema

A Mongoose schema is used to define the structure of a document, value types, default values, etc.

Check out the schema type [documentation](https://mongoosejs.com/docs/schematypes.html) for more information about schemas in mongoose.

An example of a mongoose schema:

```js
const mongoose = require("mongoose");

// by initializing a new schema it is possible to create a document that would hold user information
const userSchema = new mongoose.Schema({
  email: { type: String, required: true, unique: true },
  name: { type: String },
  age: { type: Number },
  password: { type: String, required: true },
  phoneNumber: { type: Number },
});

const dataTypeSchema = new mongoose.Schema({
  string: { type: String },
  number: { type: Number, min: 18, max: 65 },
  arrayOfNumbers: [{ type: Number }],
  object: { type: mongoose.Schema.Types.Mixed },
  date: { type: Date, default: Date.now },
});

// it is possible to type the field type directly if there are no other options needed
const dataTypeSchema2 = new mongoose.Schema({
  string: String,
  arrayOfNumbers: [Number],
  object: mongoose.Schema.Types.Mixed,
  arrayOfObjects: [mongoose.Schema.Types.Mixed],
  arrayOfArrayOfStrings: [[String]],
});
```

### Mongoose model

A mongoose model can provide us with an interface to interact with the database by creating, updating, querying, and deleting the records from said database.

Check out this [link](https://mongoosejs.com/docs/api/model.html) for more information about the model and it's method

An example on a mongoose model:

```js
const mongoose = require("mongoose");

// by initializing a new schema it is possible to create a document that would hold user information
const userSchema = new mongoose.Schema({
  email: { type: String, required: true, unique: true },
  name: { type: String, required: true, unique: true },
  password: { type: String, required: true },
  phoneNumber: { type: Number },
});

// create and export the mongoose model
module.exports = mongoose.model("User", userSchema);
```

```js
const express = require("express");
const port = 3000;

const app = express();

// require the model to use it
const userModel = require("./userSchema");

app.use(express.json());

app.post("/create/user", (req, res) => {
  const { email, name, age, password, phoneNumber } = req.body;

  const user = new userModel({
    email, // same as typing email: email
    name,
    age,
    password,
    phoneNumber,
  });

  // using promisees to save a user
  user
    .save()
    .then((result) => {
      // result is the user record after being saved in the database,
      // it will come back with a new field `_id` which is an
      // auto generated id for this document
      res.json(result);
    })
    .catch((err) => {
      res.send(err);
    });

  // using async and await to save a user, make sure to add async to the function to be able to use await
  // try {
  //   const newUser = await user.save();
  //   res.json(newUser);
  // } catch (err) {
  //   // throw err;
  //   res.send(err);
  // }
});

app.get("/users", (req, res) => {
  // `.find({})` is used to retrieve all the documents, returns an array
  userModel
    .find({})
    .then((result) => {
      res.send(result);
    })
    .catch((err) => {
      res.send(err);
    });
});

app.listen(port, () => {
  console.log(`Example app listening at http://localhost:${port}`);
});
```

### Querying

Querying is used to filter the retrieved data depending on the search query

```js
const userModel = require("./userSchema");

// `findOne` returns one document that matches the search query
userModel.findOne({ email: "John@gmail.com" }); // find the users with the email "John@gmail.com"

userModel.find({ age: 25, name: "John" }, "name age"); // find all users with the age 25 and name "John" and return the name and age fields only

userModel
  .find({ name: "John" })
  .where("age")
  .gt(20)
  .lt(50) // the up to this point it will return all the users who are called "John" and have an age between 20-50
  .sort({ age: -1 }) // sort will sort the documents in a descending order since the value is -1, it was 1 then it would sort it in an ascending order
  .select("name age") // select will select the fields to return from the query
  .exec() // exec will run the query
  .then((result) => {
    res.send(result);
  })
  .catch((err) => {
    res.send(err);
  });

// another way to create complex queries
// comparison query operators in mongodb | https://docs.mongodb.com/manual/reference/operator/query-comparison/
//  age: { $lt: 10 }    age less than 10
//  age: { $lte: 10 }   age less than or equal to 10
//  age: { $gt: 10 }    age greater than 10
//  age: { $gte: 10 }   age greater than or equal to 10
userModel.find({ age: { $lt: 50 } }); // find all users with the age less than 50

//  logical query operators | https://docs.mongodb.com/manual/reference/operator/query-logical/
//  { $and: [{ age: { $lt: 50 } }, { age: { $gt: 20 } }] }   all queries in the array should apply to return the record
//  { $or: [{ age: { $lt: 20 } }, { age: { $gt: 30 } }] }    one of the queries in the array should apply to return the record
userModel.find({ $and: [{ age: { $lt: 50 } }, { age: { $gt: 20 } }] }); // find all users whose age is less than 50 and more than 20
```

### Pulse Check

1. Create the following files and install `mongoose` and `express`.

   1. schema.js file

      ```js
      const mongoose = require("mongoose");
      ```

   2. db.js

      ```js
      const mongoose = require("mongoose");
      ```

   3. app.js

      ```js
      const express = require("express");
      const todoModel = require("./schema");
      const db = require("./db");

      const app = express();
      app.use(express.json());

      app.get("/todos", (req, res) => {});
      app.post("/create/todo", (req, res) => {});
      app.put("/update/todo", (req, res) => {});
      app.delete("/delete/todo", (req, res) => {});

      const port = 3000;
      app.listen(port, () => {
        console.log(`Example app listening at http://localhost:${port}`);
      });
      ```

2. Create a database connection in `db.js`.

3. Write a schema for a todo list that will hold the following information: `task`, `description`, `deadline`, `isCompleted`, and `priority`. Read this [link](https://mongoosejs.com/docs/schematypes.html) to know more about the schema data types.

4. Connect mongoose model to the schema and export it so that it can be used in `app.js`.

### Practice

1. Complete the API for creating a new todo list item, save the new todo item and send back a response of the newly saved item.

2. Use MongoDB Compass to preview your database after adding data to the database.

3. Complete the API for getting all of the todo list items from the database, find all the todos and send back a response of all the todos.

4. Create an API for getting all the completed todos.

5. Complete the API for updating the todo list item. Search the mongoose [documentation](https://mongoosejs.com/docs/api.html) to learn how to update a record in the database.

6. Complete the API for deleting the todo list item. Search the mongoose [documentation](https://mongoosejs.com/docs/api.html) to learn how to delete a record in the database.
