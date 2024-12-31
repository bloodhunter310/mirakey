# Cascading Style Sheet Part 1 (CSS)

## High Level Goals

By the end of this lesson, you will be familiar with the following:

- The definition of CSS
- Using different ways to style the page
- CSS selectors

## CSS

### What Is CSS

Cascading Style Sheets are used to format the layout of Web pages by describing how HTML elements are displayed.

CSS can modify HTML elements in many way such as changing the color, size, font, margins, paddings and much more, there are multiple ways of using CSS, each has it is own pros and cons but the best way to use CSS is by creating an external file for it then link it with the HTML.

### CSS Rules

CSS rules are made of two sections, the CSS selector and the declaration block.

Selectors are the patterns that are used to target a specific element or group of elements to style.

Declaration block is Where the CSS properties and values are added and separated by semicolons CSS properties and their values are representing in a key-value pair similar to objects.

Examples on Selectors:

<details>
  <summary>
    Tag Selector:
  </summary>

```html
<h1>Hello World</h1>
```

```css
/* to select an element by the tag name all you need to do is type the name of the tag name followed by curly brackets  */
h1 {
  /* the declaration block is what is in between the curly brackets */
  color: red;
}
```

<hr>
</details>

<details>
  <summary>
    Class Selector:
  </summary>

```html
<!DOCTYPE html>
<html>
  <body>
    <!-- the class name is defined in the class attribute in the HTML tag,
    it is possible to add multiple classes by leaving a space in between -->
    <h1 class="heading">Hello World</h1>
    <p class="blue big">Hello World Hello World !!!</p>
  </body>
</html>
```

```css
/* in order to select a class by it's name, add a dot before the class name, as in `.class-name{}` */
.heading {
  color: red;
  text-align: center;
}

.blue {
  color: blue;
}

.big {
  font-size: 20px;
}
```

<hr>
</details>

<details>
  <summary>
    ID Selector:
  </summary>

```html
<!DOCTYPE html>
<html>
  <body>
    <!-- the id name is defined in the id attribute in the HTML tag, each element should have one id at max -->
    <h1 id="header">Hello World</h1>
    <p id="paragraph">Hello World Hello World !!!</p>
  </body>
</html>
```

```css
/* in order to select an ID by it's name, add `#` sign before the ID name, as in `#id-name{}` */
#header {
  color: red;
  text-align: center;
}

#paragraph {
  color: white;
  font-weight: bold;
}
```

<hr>
</details>

### Some CSS Attributes

<details>
  <summary>
    Font size/weight/family
  </summary>
 it is possible to customize the font using the following css attributes

```css
p {
  /* font-size controls the size of the font, it's value can be in pixels or other units such as rems (1rem = 16px) */
  font-size: 21px;
  /* font-weight decides the weight of the font, meaning how thick or thin the characters in the text should be  */
  font-weight: bold; /* normal|bold|bolder|lighter|100-200-300-400-500-600-700-800-900|initial|inherit; */
  /* font-family is used to change the font, it is possible to pick multiple fonts and depending on what is available it will be picked in order 
  there are five generic font families that all fonts belong to them, Serif, Serif, Monospace, Cursive, Fantasy, it is possible to use the font family name of the name of the 
  font that belongs to one of these families like arial, times new roman, helvetica etc */
  font-family: sans-serif;
}
```

</details>

<details>
  <summary>
    Color:
  </summary>

The color attribute decides the color of the text that is used inside the element, the color value could be assigned in different ways.

```css
/* using built in values such as red, black, white, blue, navy, teal, purple and so on */
body {
  color: red;
}

/* using hexadecimal color codes:
hexadecimal codes consist of three bytes hex numbers which means that they consist of six digits and each pair of these digits represents the intensity of (R,G,B) in the color,
since modern browsers support the full spectrum of 24-bit color, there are 16,777,216 different color possibilities */
h1 {
  /* ff is the highest intensity of color (white) */
  color: #ffffff;
  /* 00 is the lowest intensity of color (black) */
  color: #000000;
  /* color red */
  color: #ff0000;
  /* color green */
  color: #00ff00;
  /* color blue */
  color: #0000ff;
}

/* RGB is similar to the hexadecimal color codes, it have three sections, each one represents one of the colors (RGB)
0 represents the lowest intensity of color and 255 represents the hightest intensity of color.
*/
p {
  color: rgb(0, 0, 255);
}

/* RGBA is similar to RGB it represent four sections, the first three sections represent the (RGB) colors same as above and the fourth one represents the alpha channel (the opacity of the the color) the range of the opacity value is in between zero and one, if the value is zero it means that it has the lowest opacity (transparent) and if it is one then it means it has the highest opacity */
span {
  color: rgba(0, 0, 255, 0.3);
}
```

<hr>
</details>

<details>
  <summary>
    Border:
  </summary>
  The border property allow you to specify the style, width, and color of an element's border.

```css
div {
  /* border style decides how would the border look like */
  border-style: dotted;
  border-style: dashed;
  border-style: solid;

  /* border width decides how thick the border will be */
  border-width: 5px;
  border-width: medium;

  /* border color will decide the color of the border */
  border-color: red;
}

p {
  /* border property can decide the width, color and style of the border */
  border: 3px solid black;

  /* it is possible to add the border only to one side of the element by using left, right, top, right */
  border-left: 3px solid black;
}
```

<hr>
</details>

<details>
  <summary>
    Margin:
  </summary>
  Margins are the spaces around the element, margins exist outside any defined borders for the element.

```css
/* margin creates a space around the element depending on the side it is created in */
div {
  margin-top: 50px;
  margin-bottom: 100px;
  margin-right: 150px;
  margin-left: 80px;
}

/* top => right => bottom => left */
p {
  margin: 5% 2% 5% 3%;
}
```

<hr>
</details>

<details>
  <summary>
    Padding
  </summary>
Paddings are the spaces around the element's content, paddings exist inside of any defined borders for the element.

```css
/* margin creates a space around the element's content depending on the side it is created in */
div {
  padding-top: 10%;
  padding-right: 20px;
  padding-bottom: 20px;
  padding-left: 10px;
}

/* top => right => bottom => left */
p {
  padding: 5% 2% 3% 5%;
}
```

<hr>
</details>

<details>
  <summary>
    Height and Width
  </summary>
 Height and Width are used to determine the height and width for elements.

```css
/* use pixels to specify the height or width */
div {
  height: 300px;
  width: 200px;

  /* background-color sets the background color for the HTML elements */
  background-color: red;
}

div {
  /* `%` is used to allocate the size depending on the parent container, so if the parent container has the 
  height of 200px then 50% will be 100px*/
  height: 50%;
  width: 100%;
}

div {
  /* `vh` (view height) and `vw` (view width) depend on the current size of the window displaying the element
  100vh is equal to the whole height of the view  */
  height: 100vh;
  width: 100vw;
}
```

<hr>
</details>

### Pseudo classes

Pseudo classes to change the style depending on the state of the selected element, some of these states are

Examples on some of the element states:

<details>
  <summary>
    Hover
  </summary>
 When hovering with the mouse over an element it's state will be changed to hover

```css
/* when any h1 is hovered change the color to red */
h1:hover {
  color: red;
}

h2:hover {
  /* change the cursor for the mouse to be a pointer to indicate that the element is clickable */
  cursor: pointer;
}
```

<hr>
</details>

<details>
  <summary>
    Active
  </summary>
 When clicking an any element it changes it's state to active and it stays active as long as the user keeps holding the click, it is mainly used with anchor tags.

```css
/* when the element is active change the color to red */
a:active {
  color: red;
}

button:active {
  background-color: red;
}
```

<hr>
</details>

<details>
  <summary>
    Disabled
  </summary>
  Disabled is used to change the style for elements that are disabled, to disable an element like a button add the disabled attribute .

```css
/* change the color to red when disabled */
button:disabled {
  color: red;
}
```

<hr>
</details>

<details>
  <summary>
    Visited
  </summary>
  If an anchor link has been open before then it gets the state of visited

```css
/* change the color to green when disabled */
a:visited {
  color: green;
}
```

<hr>
</details>

### Where to use CSS

CSS can be used to style the HTML page in different ways, here are some of the ways to apply CSS:

#### Internal CSS

Example on using internal CSS:

```html
<!DOCTYPE html>
<html>
  <head>
    <!-- for internal CSS the styling should be in the style tag -->
    <style>
      body {
        font-family: Arial, Helvetica, sans-serif;
        color: white;
        background-color: black;
      }
      h1 {
        font-weight: bold;
        color: #d8c40d;
      }
    </style>
  </head>
  <body>
    <h1>Hello World</h1>
  </body>
</html>
```

#### Inline CSS

Example on using inline styling:

```html
<body>
  <!-- for inline styling add the CSS properties and values directly to a style attribute on the desired element  -->
  <h1 style="color:blue; font-size:22px;">Hello World</h1>
</body>
```

#### External CSS

Example on using external styling:

```css
/* style.css */
body {
  background-color: black;
  color: white;
}
```

```html
<!DOCTYPE html>
<html>
  <head>
    <!-- connect the html page with a CSS page using the link tag, whatever styles are in the CSS file they will be applied to the HTML page -->
    <link rel="stylesheet" type="text/css" href="style.css" />
  </head>
  <body>
    <h1>Hello World</h1>
  </body>
</html>
```

The preferred way of styling is using External CSS, it is cleaner when having the style separate from the HTML page also it is possible to reuse the same style sheet with other pages.

### CSS Rule Priorities

The more specific the CSS rule is, the higher priority it has, an inline style is more specific than a tag selectors so if there are similar CSS properties, the one that would override the other would be the inline style rule.

when it comes to classes and IDs the same rules applies an inline is more specific than an ID, an ID is more specific than a class and a class is more specific than a tag selector, there is an exception though, if the keyword `!important` is used then it would override other similar properties regardless of the location of the rule.

Example on the keyword important:

```css
body {
  /* by using the keyword important it will override any other color properties in the body */
  color: red !important;
}
```

### Practice

1. Create a new CSS file with the extension of `.css`, and connect it to a new HTML page using the link tag.

2. Change the background color and the text to the color of your choosing.

3. Create an unordered list with three items, `Home`, `About`, `Contact`, then change the background color for the `ul` to be a different color than the `body`, add an anchor tags around all the list items and give the href attribute the value of `#`(Doesn't link it to anything).

4. read about `text-decoration` and remove the underline from the anchor tag in the list items.

5. add an on hover pseudo class on the anchor tags that changes their color to `#4a77b5` also when visited change the color to `#173359`.

6. read about `display` CSS property and display the list items horizontally then read about `float` and display the third list item `Contact` on the right side while everything else is on the left.

7. Add an image and make it circular, read about the `border-radius`property.

8. Add a multi line paragraph, and read about `line-height`, and change the `line-height`, `font-size`, `font-family` and `color`.
