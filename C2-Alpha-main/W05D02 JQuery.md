# JQuery

## High Level Goals

By the end of this lesson, you will be familiar with the following:

- JQuery
- DOM manipulation using jQuery

## What Is jQuery

JQuery is a light weight, and feature-rich javaScript library that makes development with vanilla JavaScript simpler.

JQuery is capable of doing many things but for this lesson we will be focusing on the DOM manipulation and event handling features.

### How To Use JQuery

There are multiple ways for using jQuery and the easiest way to use it is by using a content delivery network (CDN), open the following [link](https://code.jquery.com/) to get jQuery, copy the `script` tag for the latest jQuery version and paste it in the `head` tag in the html page.

To test if jQuery is working properly open the console and type `jQuery` or `$` which is just a shorthand for `jQuery`, the `$` function will be used every time we try to use a method from jQuery.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <script
      src="https://code.jquery.com/jquery-3.6.0.js"
      integrity="sha256-H+K7U5CnXl1h5ywQfKtSj8PCmoN9aaq30gDh27Xc0jk="
      crossorigin="anonymous"
    ></script>
  </head>
</html>
```

### DOM Manipulation Using JQuery

#### Selecting HTML Elements

to select an HTML element we use the `$` function and pass to it the selector.

```js
const body = $("body");
const listItems = $("li");

const hero = $("#hero");
const callToAction = $("#hero button");

const container = $(".container");
```

#### Modifying HTML Attributes

```js
const body = $("body");
// set the new html value using html method
body.html("");
// invoking the html method without passing an argument returns the value instead of setting it
body.html(); // => ""

const header = $("#header");
header.text("Hello World");
// you can also use the text method to return the current value of the text
header.text(); // => ("Hello World"

// to add classes add one or more class names separated by space in the `addClass` method
header.addClass("Main-Header blue-bg");
// to remove a class add one or more class names separated by space in the `removeClass` method
header.removeClass("blue-bg");
// to add styling use the `css` method
header.css("color", "red");
// pass an object to `css` method to add or modify multiple css attributes at once
header.css({
  "font-size": "50px",
  color: "blue",
});

// `hide` method is used to hide the element
header.hide();
// `show` method is used to show the element if hidden
header.show();
```

#### Creating and Removing HTML Elements

```js
// to create a new element pass in the tag to the `$` function
const paragraph = $("<p> Hello there </p>");
paragraph.
// it is possible to type nested tags with attributes such as id, class, href, etc
const navBar = $(`<div id="nav"> <div >Logo</div> <div> <a href=#> home </a> <a href=#> about </a> </div> </div>`);
navBar.css("display", "flex")

// add elements using the `append` or `appendTo` methods
const body = $("body");
// both lines below will add the paragraph as the last child to the body
body.append(paragraph)
paragraph.appendTo(body)
// both lines below will add the paragraph as the first child to the body
body.prepend(navBar)
navBar.prependTo(body)

// use the `remove` method to delete the elements from the DOM
paragraph.remove()
```

#### Adding Event Listeners

```js
// selecting the elements with the `listItem` class
const listItems = $(".listItems");
// it is possible to use the `on` method to attach event listeners on elements
// the code below will attach the click event on every selected element
listItems.on("click", () => {
  console.log("List item has been clicked");
});

// on hover change the color to red
listItems.on("mouseover", function () {
  // $(this) refers to the element it self, to have the correct reference use ES5
  $(this).css("color", "red");
  console.log("color has been changed");
});

const mainHeader = $(".main-header");
mainHeader.on("click", () => {
  console.log("Main header has been clicked");
});
```

#### Removing Event Listeners

```js
// .off removes all event listeners from all the selected buttons
$("button").off();

// .off removes all click event listeners from all the selected buttons
$("button").off("click", "**");
```

### Practice

0. Solve the questions below using jQuery, DO NOT use vanilla javascript for DOM manipulation (selecting, creation, modifying, etc).

1. Create an empty HTML page and connect it to a JavaScript file by using a script tag.

2. Using jQuery create two new elements when the page loads, a header saying `Todo List` and an empty unordered list below it.

3. Create a `toDos` global variable holding three `to do` items, `wake up`, `eat breakfast`, and `code`.

4. Create a function `renderList` that renders the todo items from `toDos` as list items in the unordered list, make sure that the function is dynamic and that it gets invoked at when while loading the page.

5. Using jQuery create an input and a button. When clicking on the button it should invoke a function `addToList` that will use the input's value to add it to the `toDos` variable. Make sure to render it on the screen as a new list item in the unordered list.

6. Create a button next to every list item that would delete the corresponding element by invoking a function `deleteListItem`. Make sure to try deleting on multiple items and check if the right item is being deleted every time.

7. Using jQuery create a new button for each list item. The button should invoke a function `updateListItem` that will ask the user for input and takes the value provided by the user to use it to update the corresponding list item.
