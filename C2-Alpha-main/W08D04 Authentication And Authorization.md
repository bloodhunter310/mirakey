# Authentication And Authorization

## High Level Goals

By the end of this lesson, you will be familiar with the following:

- Authentication
- Authorization
- Hashing
- Environment variables
- JWT

## Authentication VS Authorization

Even though authentication and authorization seem to be similar in meaning, they are completely different. They depend on each other, authentication is basically the verification of the user's credentials that can come in a variety of different forms such as passwords, one-time pins, biometrics, or authentication apps, and authorization is the process of granting and denying permissions depending on whether the authenticated user is authorized to do a certain action or not, usually done through settings.

### Authentication

An example of authentication would be the login process to verify if the user is valid or not. After the user submits the registration information in the back-end the password will be hashed and saved in the database. Then when the user logs in the next time and sends the login information to the back-end, the back-end will check if that user exist in the database and if yes then it will compare the decrypted password with the submitted one. If the passwords match, it means that the user is valid and a response will be sent stating that.

### Authorization

An example of authorization would be giving specific permissions to specific users, for example, an admin user would have more permissions than a normal user. Permissions are used to set rules for the users on what they can and can't do. Some basic permissions would be `read`, `write`, `update`, and `delete`. Let's say that a user `student` tried to access a part of an application, although that part is only for users with the role of `teacher`. That means that the student isn't authorized to do that action and will be denied from accessing that part.

NodeJS enable us to implement authorization by using middleware on the routes we are protecting.

## Hashing

Hashing is used to turn some text into a unique text digest by using some hashing algorithms and since hashing is a one way function there is no way to reverse the hashing process. Reversing it would need a lot of computing power. When hashing passwords it is good practice to add a salt which is a unique value that is added to the hash for more security.

We will be using an NPM package called [bcrypt](https://www.npmjs.com/package/bcrypt) to hash a password and compare the hashed password with an un-hashed one.

An example on using bcrypt:

```js
const bcrypt = require("bcrypt");

// hashing method
// password => my_secure_password
// salt => 10
bcrypt.hash(password, salt, (err, hash) => {
  // the parameter hash represents the hashed password
  // hash => 2c9a8d02fc17ae77e926d38fe83c3529d6638d1d636379503f0c6400e063445f
});

// comparing method
bcrypt.compare(password, hashedPassword, (err, result) => {
  // result will be a boolean depending on whether the hashedPassword is made using the password provided
});
```

### Environment variables

Since users can't be trusted, we can't share any sensitive information like API keys, salt, secrets, database credentials, or any secure information that the users shouldn't have access to, hence we need to find a way to hide it from the users and not add it directly to our code. Ona way of doing this is with the use of environment variables. An environment variable is a variable that is set outside the application, usually through a functionality built into the operating system.

We will be using [dotenv](https://www.npmjs.com/package/dotenv) to manage our environment variables instead of adding the variables by using the operating system.

An example on dotenv:

1. Using a `.env` file to hold the information. Make sure to add it to `.gitignore`.

   ```txt
   DATABASE_HOST=localhost
   DATABASE_USER=root
   DATABASE_PASS=123456
   SECRET=kjhfdshk124oip
   ```

2. Using a JavaScript file.

   ```js
   const express = require("express");
   const app = express();
   // initializing the config to be used in the application
   // if any of the required has an env variables and is required before the config then it will return undefined, so make sure to use the config before requiring the files that would use it
   require("dotenv").config();

   //getting the value from the environment, the same way is used to access variables that are set by using the operating system
   console.log(process.env.DATABASE_HOST); // => localhost
   console.log(process.env.SECRET); // => kjhfdshk124oip

   const PORT = 3000;
   app.listen(PORT, () => console.log(`listening at http://localhost:${PORT}`));
   ```

### JSON Web Token (JWT)

A JWT is hashed information that is used mainly for authentication, authorization and information exchange. JWTs are tokens issued by the server to indicate that the user is valid and are later saved in the client-side (local storage, cookies), being sent with every request. As long as the signature is correct, the information can be trusted. Even though JWT are encrypted they are not secure so it isn't a good way to save sensitive information such as passwords. A JWT consists of three parts that are separated by dots and it would look something like this:

`eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJuYW1lIjoiSm9obiBEb2UifQ.DjwRE2jZhren2Wt37t5hlVru6Myq4AhpGLiiefF69u8`

The first part contains the header information such as the algorithm, the type, and the issuer.

The second part consists of the payload which is the information that is sent to the client such as the username or email, and so on.

The third part is the signature which is made by using the previous information along with the secret key for the application. Since it was created in this way, if any part changes, such as the payload as an example, then it will invalidate the signature hence the only way to fake a payload is if the secret key is made public. Then people could use it to send fake information to the server.

![jwt](./illustrations/W08D03/jwt.png)

for more information about JWT check out the following links [jwt](https://jwt.io/). and [jsonwebtoken](https://www.npmjs.com/package/jsonwebtoken)

An example on using JWT:

```js
const jwt = require("jsonwebtoken");

// getting environment variables
const SECRET = process.env.SECRET;
const TOKEN_EXP_Time = process.env.TOKEN_EXP_Time;

// generating a new token
const generateToken = () => {
  // the payload that will be sent to the client-side
  const payload = {
    id: 1,
    permissions: ["r", "w"],
    type: "user",
  };

  const options = {
    expiresIn: TOKEN_EXP_Time,
  };
  return jwt.sign(payload, SECRET, options);
};

const authenticateToken = (token) => {
  // verifying the token by using the secret key
  const parsedToken = jwt.verify(token, SECRET);
};
```

### Authentication & Authorization System

#### Sign up

- Before saving the new user make sure to hash the password by using `bcrypt.hash`.
- It is possible to use the `pre` hook to hash the password before saving it.

#### Sign in

1. Use the provided `username` or `email` to find the `user` from the database.

2. If the `user` is found then use `bcrypt.compare()` to compare the received password with the saved hashed password.

3. If the passwords match then generate a JWT using `jwt.sign()` with the needed payload and options.

4. After generating the JWT send it back to the font-end.

5. Make sure to do error handling if the `user` doesn't exist or the password didn't match.

#### Sending JWT With Requests

- Using postman: in the Authorization tab pick `Bearer Token` as the `type` and then add the JWT in the allocated input for the `token`.

  ![bearer](./illustrations/W08D03/bearer.jpg)

- Axios request: get the token from the saved location (local storage) and add it as a header for the request, keep in mind that different HTTP methods have different locations for adding the header.

  ```js
  // if the token was stringified then it needs parsing
  const token = JSON.parse(localStorage.getItem("token"));

  // headers can be set in the second parameter for the get method
  axios.get("http://localhost:3000/users", {
    headers: {
      authorization: "Bearer " + token,
    },
  });

  // headers can be set in the third parameter for the post method
  axios.post(
    "http://localhost:3000/create/user",
    {
      email: "email@gmail.com",
      password: "12345678",
    },
    {
      headers: {
        authorization: "Bearer " + token,
      },
    }
  );
  ```

#### Middleware Authentication

1. Create a middleware function with access to `req`, `res` and `next`.

2. Check `req.headers.authorization` for a bearer token.

3. If it exist it will be in a string similar to this one `Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJuYW1lIjoiSm9obiBEb2UifQ.DjwRE2jZhren2Wt37t5hlVru6Myq4AhpGLiiefF69u8` since we need the token only we could do `const token = req.headers.authorization.split(" ").pop()` to save the token in a variable.

4. Verify the token using `jwt.verify()` and if it is a valid token then use the `next` function.

5. Make sure to send back a response in case that the token was missing or it was not valid.

6. Export the middleware function and use it for specific routes that need a logged in user to be accessed.
