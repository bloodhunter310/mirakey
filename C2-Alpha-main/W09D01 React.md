# React JS

## High Level Goals

By the end of this lesson, you will be familiar with the following:

- React
- React Components
- Passing Props To Child Components

## React

React is a JavaScript library for building the client-side, React allows to build complex UI by using smaller isolated pieces that are called components.

### Installing And Setting Up A React Project

We are going to use `create-react-app` to work with react and reduce the amount of time it is used to setup a project, to use it just run the following command `npx create-react-app app-name` then to run the created app `cd` into the react app directory then run `npm start`.

Since we will be learning react with class components then we will have to change some code from the generated project.

### Create React App File Setup

Here is a quick guide that explains some of the files that gets generated when using `create-react-app`.

- `client/index.html`: it's the main html page that holds the div that react gets rendered in.
- `src/index.js`: has the code responsible for rendering react in the div with the id `root` that exist in the index.html page.
- `src/App.js`: its the main component that gets rendered in the `root` div.

### JSX

JSX stands for JavaScript XML and it is used write HTML elements in React.

There are other ways to create HTML elements in React like using `React.createElement()` but since JSX is way more convenient to use and it is the best practice for using react then there is no need for dealing with the other ways.

### React Functional Components

There are two ways of creating components in react `class components` and `functional components`. We will be learning the functional component first along side its hooks.

A functional component in short is made out a function that is returning JSX, it can use react hooks (more on that in a later lesson).

When creating functional components make sure that the function starts with a capital letter like classes, and the same goes when naming the files that components exist in.

```js
import React from "react";

const App = () => {
  // we can setup variables at the start of the function
  const name = "John";
  const age = 25;

  // return must return one JSX element that can have multiple nested children
  return (
    // the empty tag called react fragment, we have used it here to wrap the nested children together, we can use other tags such as `div`
    <>
      <h1>Header</h1>
      <p>Paragraph</p>

      {
        // to add javaScript in JSX use curly brackets `{}`
        console.log("Hello")
      }

      {`My name is ${name} and i am ${age} years old`}
    </>
  );
};

export default App
```

### Child Components

Since react is component based then it makes sense that some components will user other components as a building block.

Header.js

```js
import React from "react";

// the component is exported so it can be imported and used in another component
export const Header = () => {
  // since we are returning one element then there is no need to wrap it with another container
  return <h1>This is a component called Header</h1>;
};
```

App.js

```js
import React from "react";
// importing the Header component so it can be used in the current component
import { Header } from "./components/Header";

const App = () => {
  return (
    <>
      <Header />
      <Body />
    </>
  );
};

// it is possible to define other components in the same file
const Body = () => {
  return <h1>This is a component called Body</h1>;
};

export default App
```

### Dynamic Rendering

When creating dynamic applications one of the most important parts is knowing how to render a list of any size, here are examples below on how to achieve that.

```js
import React from "react";

const App = () => {
  const numbers = [1, 2, 3, 4].map((element, index) => {
    return (
      // the key prop (attribute) below is used so react identifies which items have changed , added or removed and it should be a unique key, preferably some sort of id and as a last resort it is possible to the index even though it isn't the most optimal for performance
      <div key={index}>
        <h4> {`Header ${element}`} </h4>
        <p> {`Element: ${element} Index:${index}`} </p>
      </div>
    );
  });

  return (
    <>
      {
        // we can directly render arrays
        [1, 2, 3, 4]
      }

      {
        // if we have an array of JSX elements then we can render it by simply referencing the array
        // the array below will be rendered as three paragraphs on top of each other (since paragraphs are block elements)
        [<p key="id_1"> 1 </p>, <p key="id_1"> 2 </p>, <p key="id_3"> 3 </p>]
      }

      {
        // we can use and define map at the start of the component and use it inside the render
        numbers
      }

      {
        // we can directly create an expression using map
        [4, 5, 6, 7].map((element, index) => {
          return <h4 key={index}> {`Header ${element}`} </h4>;
        })
      }
    </>
  );
};

export default App
```

### Passing Props

To make React more dynamic we need a way to pass information from one component to another, and we can do that easily and similarly to adding HTML attributes.

```js
import React from "react";

const App = () => {
  const listItems = ["item one", "item two", "item three"];

  return (
    <>
      <h4> List </h4>
      {/* below we are passing a prop called collection with the value of listItems*/}
      <List collection={listItems} />
      <Button type="submitButton"> Add To List </Button>
    </>
  );
};

const List = ({ collection }) => {
  return (
    <>
      <ul>
        {collection.map((element, index) => {
          return <li key={index}> {element} </li>;
        })}
      </ul>
    </>
  );
};

const Button = ({ type, children }) => {
  console.log(type);
  return <button> {children} </button>;
};

export default App
```

### Event Handling

```js
import React from "react";

const App = () => {
  const handelSubmit = (e) => {
    console.log(e.target);
  };

  const handelChange = (e) => {
    console.log(e.target.value);
  };

  return (
    <>
      <button onClick={handelSubmit}> Add To List </button>
      <button
        onClick={(e) => {
          console.log(e.target);
        }}
      >
        Add To List
      </button>

      <input onChange={handelChange} />
      <input
        onChange={(e) => {
          console.log(e.target.value);
        }}
      />
    </>
  );
};

export default App
```

### Pulse Check

1. Create a react app called `react_todo_list` using `create-react-app`.

2. Modify the app component so it returns a `div` containing an `h1` saying `hello world`.

3. Create a new folder called `components` in the `src` directory.

4. Create a new file called `List.js` in the `components` directory then create and export a component called `List`.

5. Create and export another component called `ListItem` and save it in `src/components`.

6. Create an array called `todos` in `App.js` with three todo elements `[{todo: "wake up", id: 1}, {todo: "breakfast", id: 2}, {todo: "study", id: 3}]`.

7. Import `List` component in `App` component and use it there then pass the `todos` array as a prop to `List` component.

8. In `List` component use destructuring on the incoming props (the `todos` array) and render an empty unordered list.

9. Modify `ListItem` component to accept two props `todo` and `id` and it should return the passed prop `todo` in an `li` tag.

10. Modify `List` component to iterate over the `todos` prop and use the `ListItem` component to render all the todos from the array.

11. Modify `ListItem` to console log the todo `id` when clicking on the corresponding `li`.
