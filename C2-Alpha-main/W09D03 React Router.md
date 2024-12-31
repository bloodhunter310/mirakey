# React Router

## High Level Goals

By the end of this lesson, you will be familiar with the following:

- React Router Dom
- Routes
- Router Hooks

## React Router Dom

Routing allow us to create more dynamic websites that shows different data depending on the provided URL, to implement routing with react it will require the use of an external library `react-router-dom`. To install react router dom using use the following command `npm install react-router-dom`

Check this [link](https://reactrouter.com/web/guides/quick-start) to open the documentation for `react-router-dom`.

### Implementing Routing

React is capable of watching specific variables that when changed will result in re-rending the component and it is possible through using the `useState` hook, the state hook is great for handling reactive data (data that changes) it will update the UI when a change occur to reflect them to the user.

Keep in mind that react also would re-render a component if the prop has changed also so this behavior isn't only exclusive for the `useState` hook.

The `useState` hook returns a variable and a function to change the value of that variable and by using array destructuring we can have access to these values `const [x, setX] = useState();`

Index.js

```js
import React from "react";
import ReactDOM from "react-dom";
// import BrowserRouter and Route
import { BrowserRouter, Route } from "react-router-dom";
import App from "./App";

ReactDOM.render(
  <React.StrictMode>
    <BrowserRouter>
      {/* render App if the path is `/` */}
      <Route path="/" component={App} />
    </BrowserRouter>
  </React.StrictMode>,
  document.getElementById("root")
);
```

App.js

```js
import React from "react";
// import Link and Route
import { Link, Route } from "react-router-dom";

const App = () => {
  return (
    <div>
      <Navigation />
      {/* render About when the path is exactly `/about`, it will not work on `/about/us` */}
      <Route exact path="/about" component={About} />

      {/* render Products if the path starts with /products, works for `/products/123` also */}
      <Route path="/products" component={Products} />

      {/* using the render prop to render ProductDetails*/}
      <Route path="/products/:id" render={() => <ProductDetails />} />
    </div>
  );
};

const Navigation = () => {
  return (
    // inline styling in react
    <div style={{ display: "flex", gap: "16px" }}>
      {/* link acts like an `a` tag */}
      <Link to="/"> Home </Link>
      <Link to="/about"> About </Link>
      <Link to="/products"> Products </Link>
      <Link to="/products/product1"> Products Details</Link>
    </div>
  );
};

const About = () => {
  return <div>About</div>;
};

const Products = () => {
  return <div>Products</div>;
};

const ProductDetails = () => {
  return <div>ProductDetails</div>;
};

export default App;
```

### Passing Props

```js
import React from "react";
// import Link and Route
import { Link, Route } from "react-router-dom";

const App = () => {
  return (
    <div>
      <Navigation />
      {/* using the render prop allows us to pass props to the component*/}
      <Route path="/products/" render={() => <Products id={1} />} />
    </div>
  );
};

const Navigation = () => {
  return (
    <div style={{ display: "flex", gap: "16px" }}>
      <Link to="/products"> Products </Link>
    </div>
  );
};

const Products = ({ id }) => {
  return <div>Product {id}</div>;
};

export default App;
```

### Using Params

```js
import React from "react";
// import Link and Route
import { Link, Route, useParams } from "react-router-dom";
import "./App.css";

const App = () => {
  return (
    <div>
      <Navigation />
      {/* defining the url parameters in the path*/}
      <Route path="/profile/:userId" component={Profile} />
    </div>
  );
};

const Navigation = () => {
  return (
    <div style={{ display: "flex", gap: "16px" }}>
      <Link to="/profile/15asd262"> Profile </Link>
    </div>
  );
};

const Profile = ({ id }) => {
  // `useParams` returns an object that contains the URL parameters
  const { userId } = useParams();
  return <div>user id: {userId}</div>;
};

export default App;
```

### Using History

```js
import React from "react";
// import Route and useHistory
import { Route, useHistory } from "react-router-dom";

const App = () => {
  return (
    <div>
      <Navigation />
      <Route exact path="/about" component={About} />
    </div>
  );
};

const Navigation = () => {
  // use the `useHistory` hook in the component to gain access to the instance that is used to navigate
  const history = useHistory();

  return (
    <div
      style={{
        display: "flex",
        gap: "16px",
        color: "blue",
        textDecoration: "underline",
      }}
    >
      <div
        style={{ cursor: "pointer" }}
        onClick={(e) => {
          // push is used to redirect to another path
          history.push("/about");
        }}
      >
        About
      </div>

      <div
        style={{ cursor: "pointer" }}
        onClick={(e) => {
          // goBack is used to go back to the previous path
          history.goBack();
        }}
      >
        Go Back
      </div>
    </div>
  );
};

const About = () => {
  return <div>About</div>;
};

export default App;
```

### Handling Undefined Routes

```js
import React from "react";
// import switch
import { Link, Route, Switch } from "react-router-dom";

const App = () => {
  return (
    <div>
      <Navigation />
      {/* switch renders the first Route child that matches the path */}
      <Switch>
        <Route exact path="/" component={Home} />
        <Route exact path="/about" component={About} />
        <Route path="/products" component={Products} />
        {/* the path `*` means any route but since switch only renders one this will not render alongside the previous routes */}
        <Route path="*" component={() => "404 NOT FOUND"} />
      </Switch>
    </div>
  );
};

const Navigation = () => {
  return (
    <div style={{ display: "flex", gap: "16px" }}>
      <Link to="/"> Home </Link>
      <Link to="/about"> About </Link>
      <Link to="/products"> Products </Link>
    </div>
  );
};

const Home = () => {
  return <div>Home</div>;
};

const About = () => {
  return <div>About</div>;
};

const Products = () => {
  return <div>Products</div>;
};

export default App;
```
