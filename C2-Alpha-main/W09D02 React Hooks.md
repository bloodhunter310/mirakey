# React Hooks

## High Level Goals

By the end of this lesson, you will be familiar with the following:

- React Hooks
- useState, useEffect and useContext

## What React Are React Hooks

React hooks are functions that are used in functional component that gives access to React state and lifecycle features

### State Hook

React is capable of watching specific variables that when changed will result in re-rending the component and it is possible through using the `useState` hook, the state hook is great for handling reactive data (data that changes) it will update the UI when a change occur to reflect them to the user.

Keep in mind that react also would re-render a component if the prop has changed also so this behavior isn't only exclusive for the `useState` hook.

The `useState` hook returns a variable and a function to change the value of that variable and by using array destructuring we can have access to these values `const [x, setX] = useState();`

```js
import React, { useState } from "react";

const Counter = () => {
  // count is the variable
  // setCount is a function to change the value of the variable
  // the argument passed to useState is the initial value for the count variable
  const [count, setCount] = useState(0);

  const inc = () => {
    setCount(count + 1);
  };

  const dec = () => {
    setCount(count - 1);
  };

  return (
    <div>
      {/* React will re-render and display the updated count automatically */}
      <p>Count:{count}</p>
      <button onClick={inc}>Increment Counter</button>
      <button onClick={dec}>Decrement Counter</button>
    </div>
  );
};

export default Counter;
```

```js
import React, { useState } from "react";

const Login = () => {
  const [email, setEmail] = useState("");
  const [password, setPassword] = useState("");

  return (
    <div>
      <p>Email: {email}</p>
      <p>Password: {password}</p>
      <input
        type="email"
        placeHolder="Email"
        onChange={(e) => {
          setEmail(e.target.value);
        }}
      />
      <input
        type="password"
        placeHolder="Password"
        onChange={(e) => {
          setPassword(e.target.value);
        }}
      />
    </div>
  );
};

export default Counter;
```

### Effect Hook

React has a lifecycle which can be accessed through the `useEffect` hook which is a function that enable the ability to perform side effects such as fetching data.

The term side effect is used when a function modifies anything outside it's own scope and in the case of react `useEffect` these side effects can affect other components and can't be done during rendering

The `useEffect` hook consists of three main sections, a callback function that runs with every render, an optional clean up function clean up function that is used to clean up side effects from the previous render, and a dependency array to control when to run the callback function and an optional lastly a tear down function that runs when the component is removed from the UI.

```js
import React, { useState, useEffect } from "react";
import axios from "axios";

const App = () => {
  const [users, setUsers] = useState();

  // if we do not add the dependency array the function will run when any stateful data changes
  // the functions will always run once when the component is initialized
  useEffect(() => {
    axios.get(`https://jsonplaceholder.typicode.com/users`).then((res) => {
      setUsers(res.data);
    });
    // an empty array dependency means there is no dependencies which will result in running the function once when initializing
  }, []);

  return (
    <div>
      {/* short circuit evaluation is being used to make sure that there is a value for the users before trying to map over it, there are other ways to do conditional rendering with react */}
      {users &&
        users.map((user) => {
          return <p key={user.id}> {user.name}</p>;
        })}
      {/* ternary operator being used to implement conditional rendering, ternary operators is similar to an if statement if the expression before the `?` is truthy then do what is on the left of the `:` otherwise do what is on the right  */}
      {users
        ? users.map((user) => {
            return <p key={user.id}> {user.name}</p>;
          })
        : ""}
    </div>
  );
};

export default App;
```

```js
import React, { useState, useEffect } from "react";
import axios from "axios";

const App = () => {
  const [status, setStatus] = useState(false);
  const [count, setCount] = useState(0);

  const toggleStatus = () => {
    setStatus(!status);
  };

  useEffect(() => {
    setCount(count + 1);
    // every time the status state changes the function will run
  }, [status]);

  return (
    <div className="App">
      <p>status: {status + ""}</p>
      <p>count:{count}</p>
      <button onClick={toggleStatus}>Increment Counter</button>
    </div>
  );
};

export default App;
```

### Context Hook

Using context hook enables the share of data without passing props to child components, it makes sharing data way more convenient in some cases like when the top level component is trying to pass down data through many child components to reach the desired component.

Using context hook allow us to bypass the drilling process and directly access it in any of the child components.

```js
import React from "react";
import Profile from "./Profile";
// import createContext
import React, { useState, createContext } from "react";

export const UserContext = createContext();

const Home = () => {
  const [user, setUser] = useState({ id: 10, name: "john" });

  return (
    <>
      <UserContext.Provider value={user}>
        <Profile />
      </UserContext.Provider>
    </>
  );
};
export default Home;
```

```js
import React from "react";
// import useContext
import React, { useContext } from "react";
// import the context
import { UserContext } from "./Home";

const Profile = () => {
  // assign the context value to a variable so it can be used
  const user = useContext(UserContext);

  return (
    <>
      <h1>{user.name}</h1>
    </>
  );
};

export default Profile;
```

### Pulse Check

1. Create a react app called `react_blog` using `create-react-app`.

2. Modify the app component so it returns a `div` containing an `h1` saying `Blog App`.

3. In the app component create a stateful variable using the state hook to hold the information of posts (`[posts, setPosts]`).

4. Add a default value for the `posts` state variable, an array with two objects with the following keys, `userId`, `id`, `title` and `body`. Make sure that the `userId` is between 1-10 and that the `id` is above 100.

5. Render the `posts` in the screen, The `title` and `body` must be visible.

6. Create a button and four inputs, each input is for one of the post keys then create a corresponding state variable for each one of the inputs.

7. Add `onChange` event for the inputs and set the input value as the value for the corresponding variable.

8. Add `onClick` event for the button that will add a new post to the `posts` variable with values of the state variables that are holding the values of the inputs.

   HINT: use the spread operator to add to the array while setting the value `setNumbers([...numbers, 10]);`

9. Use the `useEffect` hook to fetch posts from the following endpoint `https://jsonplaceholder.typicode.com/posts` and then set the `posts` variable with the value of the received posts.

   NOTE: don't forget to add an empty dependency array to prevent `useEffect` from being invoked over and over again.
