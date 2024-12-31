# Advanced Mongoose

## High Level Goals

By the end of this lesson, you will be familiar with the following:

- Mongoose Middleware
- Mongoose Statics
- Mongoose Methods
- Populate

## Mongoose Middleware

Mongoose middleware (also known as pre and post hooks) is a function that is called before or after a specific event.

There four types of middlewares that are have access to the pre and post hooks, check out this [link(https://mongoosejs.com/docs/middleware.html)] for more information about mongoose middelware.

an example on pre and post middlewares:

```js
const mongoose = require("mongoose");

const usersSchema = new mongoose.Schema({
  email: { type: String, required: true, unique: true },
  password: { type: String, required: true },
});

// we are using ES5 below because ES6 uses "lexical this" and that would change
// the value that "this" is supposed to point at which is the instance of the user

// post is executed after the findOne completes
usersSchema.post("findOne", function (result) {
  // will log the found document
  console.log(result);
});

// pre executers before the save
usersSchema.pre("save", async function () {
  // `this` refers to the newly created user before saving
  this.email = this.email.toLowerCase();
});

module.exports = mongoose.model("User", usersSchema);
```

### Mongoose Static Methods

Mongoose static methods are methods that are attached to the mongoose model itself.

```js
const mongoose = require("mongoose");

const usersSchema = new mongoose.Schema({
  email: { type: String, required: true, unique: true },
  username: { type: String, required: true, unique: true },
  password: { type: String, required: true },
});

// the findByUserName method can be called directly from the model
usersSchema.statics.findByUserName = function (username) {
  return this.find({ username }, (err, result) => {
    console.log(result);
  });
};

module.exports = mongoose.model("User", usersSchema);
```

```js
const User = require("./user_schema");

// the method is used directly from the model
User.findByUserName("JohnDoe!@#");
```

### Mongoose Methods

Mongoose methods are methods that are attached to the model instance.

```js
const mongoose = require("mongoose");

const usersSchema = new mongoose.Schema({
  email: { type: String, required: true, unique: true },
  username: { type: String, required: true, unique: true },
  password: { type: String, required: true },
});

// can be called from the model instance
usersSchema.methods.getInfo = function () {
  console.log(`username: ${this.username}, email: ${this.email}`);
};

module.exports = mongoose.model("User", usersSchema);
```

```js
const User = require("./user_schema");

// creating a new instance of the model
const user = new User({
  email: "JohnDoe@gmail.com",
  username: "JohnDoe!@#",
  password: "123456789",
});

// using the method from the instance
user.getInfo(); // username: JohnDoe!@#, email: JohnDoe@gmail.com
```

### Populate

Populating in mongoose is the process of automatically replacing some fields in the document with documents from another collection.

```js
const mongoose = require("mongoose");

const rolesSchema = new mongoose.Schema({
  role: { type: String, required: true, unique: true },
  permissions: [{ type: String, required: true, unique: true }],
});

const usersSchema = new mongoose.Schema({
  email: { type: String, required: true, unique: true },
  username: { type: String, required: true, unique: true },
  password: { type: String, required: true },
  role: { type: Schema.Types.ObjectId, ref: "Role" }, // the value of the field must be an ObjectId from Role
});

const Role = mongoose.model("Role", rolesSchema);
const User = mongoose.model("User", usersSchema);

User.findOne({ username: "John" })
  .populate("role") // we can populate specific fields if you specify them in a second argument like this, .populate("role". "role")
  .exec()
  .then((result) => {
    // result should return the user with the role information also
    console.log(result);
  });
```
