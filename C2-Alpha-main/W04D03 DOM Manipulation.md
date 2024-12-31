# DOM Manipulation Using JavaScript

## High Level Goals

By the end of this lesson, you will be familiar with the following:

- The definition of DOM
- Changing HTML elements
- Changing HTML attributes
- Modifying current CSS styles and creating new ones
- The definition of event listeners
- Using event listeners

## DOM Manipulation

### What Is The DOM

Document Object Model (DOM) is a programming interface that is used with HTML and XML documents which allows programs to change the document. Using JavaScript we could modify the HTML page, it is possible to add, delete, and update all HTML elements, attributes, events, and CSS styles.

### Selecting HTML Elements

```js
// `querySelector` allows us to get a reference to the body object so we can modify it
const body = document.querySelector("body");
// setting the display attribute to none
body.style.display = "none";

// `querySelectorAll` allows us to get all of the paragraph objects and returns an array containing a reference to them
const paragraphs = document.querySelectorAll("p");
// changing the color attribute for the first paragraph to red
paragraphs[0].style.color = "red";

// it is possible to select an element with a specific id just, add a `#` before the id name
const article = document.querySelector("#Article");

// it is possible to select all elements with a specific class, just add a `.` before the class name
const cards = document.querySelectorAll(".card");

// it is possible to use other CSS selectors with `document.querySelector` and `document.querySelectorAll`
// here it is selecting an `h1` tag that has a `div` parent
document.querySelector("div > h1");
```

### Modifying HTML Attributes

```js
// it is possible to access all of the attributes
const body = document.querySelector("body");
// setting the display attribute to none
body.style.display = "none";

const paragraphs = document.querySelectorAll("p");
// changing the color attribute for the first paragraph to red
paragraphs[0].style.color = "red";

const link = document.querySelector("a");
link.href = "https://www.google.com";
link.target = "blank";
```

### Creating and Removing HTML Elements

```js
// to create a new html element use `document.createElement` and pass in the name of the tag you want to create
const header = document.createElement("h1");

// you can modify the newly created element's attributes by accessing it and changing the attributes for the values
header.innerText = "Header One";
header.id = "header_id";

// in order to add it as a child for another element, use the `append` method
// selecting the body to append the header to it
const body = document.querySelector("body");

// specify the HTML element then execute the append method with the element you wish to add
body.append(header);

// to remove the header element use the `remove` method
header.remove();
```

### Event Listeners

Event listeners are connected to the DOM and can execute code depending on which event has triggered. An example of these events would be click, change, hover, key press, etc.

Examples on event listeners

```html
<!-- using the `onclick` attribute it is possible to attach an on click listener to the button that will execute the
 function `hello` when clicking on the button -->
<button onclick="hello()"></button>

<!-- using the `onchange` attribute it is possible to attach an on change listener to the input that will execute the
 function `hello` if any changes have happened to the inputs value -->
<input onchange="hello()" />

<script>
  const hello = () => {
    console.log("Hello");
  };
</script>
```

### Adding Event Listener With JS

```js
const submitButton = document.createElement("button");
// `addEventListener` is used to attach an event listener to an html element
// it takes two arguments the type of the event and a callback that execute when the event is triggered
submitButton.addEventListener("click", () => {
  console.log("Submit button has been clicked");
});

const profilePic = document.querySelector("#profile-pic");
// example of mouseover event
submitButton.addEventListener("mouseover", () => {
  console.log("Profile picture has been hovered");
});
```

### Remove Event LIstener

```js
const editButton = document.createElement("button");

const editUser = () => {
  console.log("editUser has been called");
};

editButton.addEventListener("click", editUser);

// `removeEventListener` takes two arguments the type of event to be removed and the reference to the function
editButton.removeEventListener("click", editUser);
```

### Event Parameter

The `event` parameter contains an object that contains information about the event that happened.

```js
const deleteButton = document.createElement("button");

const logTarget = (e) => {
  // e.target is the element that triggered the event
  console.log(`The ${e.target} has triggered the event`);
};

deleteButton.addEventListener("click", logTarget);

const emailInput = document.createElement("input");

const logValue = (e) => {
  console.log(`${e.target.value} is the current value of the input`);
};

emailInput.addEventListener("change", logValue);
```

### Practice

1. Create an empty HTML page and connect it to a JavaScript file by using a script tag.

2. Using DOM manipulation create two new elements when the page loads, a header saying `Todo List` and an empty unordered list below it.

3. Create a `toDos` global variable holding three `to do` items, `wake up`, `eat breakfast`, and `code`.

4. Create a function `renderList` that renders the todo items from `toDos` as list items in the unordered list, make sure that the function is dynamic (renders all items regardless of the size) and that it gets invoked at when while loading the page.

5. Using DOM manipulation create an input and a button. When clicking on the button it should invoke a function `addToList` that will use the input's value to add it to the `toDos` variable. Make sure to render it on the screen as a new list item in the unordered list.

6. Create a button next to every list item that would delete the corresponding element by invoking a function `deleteListItem`. Make sure to try deleting on multiple items and check if the right item is being deleted every time.

7. Using DOM manipulation create a new button for each list item. The button should invoke a function `updateListItem` that will ask the user for input and takes the value provided by the user to use it to update the corresponding list item.
