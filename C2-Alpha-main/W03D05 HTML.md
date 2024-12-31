# Hypertext Markup Language (HTML)

## High Level Goals

By the end of this lesson, you will be familiar with the following:

- The definition of HTML
- Using HTML tags
- Using attributes
- Event Listeners

## HTML

### What Is HTML

Hypertext Markup Language (HTML) is the standard markup language for documents designed to be displayed in a web browser. It can be assisted by technologies such as Cascading Style Sheets (CSS is used to customize the style of the web site) and scripting languages such as JavaScript (JavaScript is used to make a dynamic web site)

HTML elements are the building blocks of HTML pages, HTML elements are portrayed by tags and are written using angle brackets.

Example on an HTML page:

```html
<!DOCTYPE html>
<html lang="en">
  <!-- the head tag isn't displayed but it is used to add meta data or for connecting the page to other pages -->
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
  </head>
  <!-- the body tag is what is being displayed on the screen -->
  <body>
    <h1>Hello World</h1>
  </body>
</html>
```

### HTML TAGS

There are three types of HTML tags, opening tag, closing tag and self closing tag.

Most HTML elements are made with opening and closing tags, and some of them are made from only opening tags or self-closing tags.

HTML can be displayed inline and as blocks, block elements take up the whole width and push the next element below it while inline elements only take the space provided to them and it will allow other elements to be right next to it.

<details>
  <summary>
    Header Tag:
  </summary>

```html
<!-- Header tags have differed sizes from 1-6 -->
<h1>Header 1</h1>

<h2>Header 2</h2>

<h3>Header 3</h3>

<h4>Header 4</h4>

<h5>Header 5</h5>

<h6>Header 6</h6>
```

<h1>Header 1</h1>
<h2>Header 2</h2>
<h3>Header 3</h3>
<h4>Header 4</h4>
<h5>Header 5</h5>
<h6>Header 6</h6>
<hr>

</details>

<details>
  <summary>
    Paragraph Tag:
  </summary>

```html
<p>
  Lorem Ipsum is simply dummy text of the printing and typesetting industry.
</p>
```

<p> Lorem Ipsum is simply dummy text of the printing and typesetting industry. </p>
<hr>

</details>

<details>
  <summary>
    Button Tag:
  </summary>

```html
<button>Click Me!!!</button>
```

<button> Click Me!!! </button>

<hr>

</details>

<details>
  <summary>
    Input Tag:
  </summary>

```html
<input />
```

</details>

<details>
  <summary>
    Ordered list Tag:
  </summary>

```html
<!-- Ordered list is a numbered list that starts at the number 1 -->
<ol>
  <li>Wake up</li>
  <li>Eat</li>
  <li>Study</li>
</ol>
```

<ol>
  <li>Wake up</li>
  <li>Eat</li>
  <li>Study</li>
</ol>
<hr>

</details>

<details>
  <summary>
    Unordered list Tag:
  </summary>

```html
<!-- Unordered list is a bullet point list -->
<ul>
  <li>Wake up</li>
  <li>Eat</li>
  <li>Study</li>
</ul>
```

<ul>
  <li>Wake up</li>
  <li>Eat</li>
  <li>Study</li>
</ul>
<hr>

</details>

<details>
  <summary>
    Dropdown list Tag:
  </summary>

```html
<!-- Dropdown list enables the user to pick an option out of a list-->
<select>
  <option>Option 1</option>
  <option>Option 2</option>
</select>
```

</details>

<details>
  <summary>
    Div Tag:
  </summary>

```html
<!-- Div tag is used to encapsulate or to group elements together, it doesn't render anything by default -->
<div>
  <h4>Some Header</h4>
  <button>Click Here</button>
</div>
```

<hr>
</details>

<details>
  <summary>
    Script Tag:
  </summary>

```html
<!-- Script tag to use JavaScript -->
<script>
  // prompt is used to get information from the user
  const answer = prompt("What is 1 + 1?");
  if (answer !== 2) {
    alert(`Wrong answer`);
  }

  // alert is used to alert the user
  alert("Warning, This is an alert message!!!");

  const sayHello = () => {
    console.log("Hello");
  };

  // would execute the function when it reaches the script
  sayHello();
</script>
```

<hr>
</details>

### HTML Attributes

HTML attributes provide additional information about HTML elements. All HTML elements can have attributes that can customize the element further. An attribute is a key
value pair that is added to the starting tag `<h1 id="header"> This is a header </h1>`.

Examples on HTML attributes

```html
<!-- the title's value is shown when hovering over the paragraph -->
<p title="tooltip about the paragraph">This is a paragraph</p>

<!-- adding placeholder text to the input and giving it a type -->
<input type="text" placeholder="Enter Text" />

<!-- if an image name is used in the src attribute that image will be displayed, make sure the image is in the same directory as the page if the path is not specified the alt attribute value will be shown instead -->
<img src="img_name.jpg" alt="img description" />

<!-- it is possible to add a link for the specified picture in the src attribute -->
<img src="https://some_url/image.jpg" alt="img description" />

<!-- anchor tag is used to link to other websites or other elements in the HTML page-->
<!-- use url to access the specified link -->
<a href="https://www.google.com/">google</a>

<!-- use an id from the page to jump to that specific element -->
<p id="paragraph">This is a paragraph</p>
<a href="#paragraph">Go to paragraph</a>

<!-- you can add a src attribute to the script tag to connect a specific JavaScript file with the html page -->
<script src="main.js"></script>
```

### Practice

1. Create an HTML file to work on. Make sure the file extension is `.html` and add the basic tags to start working such as the `html`, `head`, and `body` tags, and give it the title `Animal Blog`.

2. Add a Header tag (h1) saying `Cute Animal Blog` then add a paragraph underneath explaining what the blog is about.

3. Add an Unordered list of your favorite animals (At least 5).

4. Add an anchor tag for every item in the list that links to an external website (wikipedia for example) with information about the animal.

5. After the list, add a header `h2` saying `gallery` then an image for each one of the animals.

6. Add a paragraph underneath every picture explaining a little bit about each animal, don't forget to add a tittle attribute with an appropriate message.

7. Create a new file `contact.html` and link to it from the main page. The contact page should have contact information (Doesn't need to be real).

   HINT: search how to link to another html page using a tag.

8. Create a new file `login.html` and link to it from the main page. The login page should contain two inputs, one of which should be an email type and the other a password type. There should also be a login button below them. Don't forget to label the inputs.

   HINT: search for input types in html and label tag.

9. Create a new file `register.html` and link to it from the login page. The register page should contain three inputs, one of which should be an email type, and two password types. Don't forget to add a register button below, and label the inputs.
