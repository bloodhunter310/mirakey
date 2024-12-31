# **Bootstrap V4**

**High-Level Goals**

By the end of this lesson, you will be familiar with the following:

- What is Bootstrap
- Installation
- Breakpoints
- Layout and Grid system
- Components

# **What is Bootstrap**

A free open-source CSS framework developed to be mobile-first, and is used to build responsive layouts and components, it contains CSS and JavaScript.

Please do know that when you use Bootstrap don&#39;t ever use CSS with it, Bootstrap will do your CSS work easily and faster.

Bootstrap is based on classes so it can be easily applied to the frontend components by adding the name of the class you want to use.

# **Installation**

There are two ways to install and use Bootstrap on your project, feel free what suits you better.

1. Through CDN for quick installation and using, by attaching the links in the head of your index.html file. Check [this link](https://getbootstrap.com/docs/5.1/getting-started/introduction/) for the CDN installation.
2. Download Bootstrap to get the compiled CSS and JavaScript, source code, or include it with your project packages. Check [this link](https://getbootstrap.com/docs/5.1/getting-started/download/) for the download installation.

# **Responsive Breakpoints**

We can describe the breakpoints as the core of how you want the responsive layout to behave.

Breakpoints divide into six sizes based on pixels from X-small to Extra extra large.

Along with breakpoints, there are media queries that are mostly based on the minimum viewport widths and are also divided into six sizes from (sm) to (xxl)

Use [this link](https://getbootstrap.com/docs/5.1/layout/breakpoints/) to check the available breakpoints table and further reading of the media queries.

# **Layout and Grid System**

The layout system is based on six tiers which means it divides the layout into six responsive tiers which you can easily shape and manipulate.
It’s built with flexbox and based on containers, rows, and columns used altogether to align content.
Along with manipulating the layout using different sizes, there are auto-layout columns that can save you a lot of work, check this link for further reading. 

It is created with HTML elements generally (div) so you add a container grid then divide the (divs) in it into rows and inside these rows you add columns, all the components will be placed inside of the columns, that will make you control the number of columns you want on each row.

For example:

```html 
<div class="container">
      <div class="row">
        <div class="col">
          <p>Lorem ipsum dolor sit amet.</p>
        </div>
        <div class="col">
          <p>Lorem ipsum dolor sit amet.</p>
        </div>
      </div>
      <div class="row">
        <div class="col">
          <p>Lorem ipsum dolor sit amet.</p>
        </div>
        <div class="col">
          <p>Lorem ipsum dolor sit amet.</p>
        </div>
        <div class="col">
          <p>Lorem ipsum dolor sit amet.</p>
        </div>
      </div>
    </div>
```

Bootstrap divides the screen into 12 columns so when you place the component inside the row without mentioning the number of columns you want each to take it will be automatically distributed in the container. However, you can easily mention the number of columns you want each element to take. 

For example: 

```html 
<div class="container">
      <div class="row">
        <div class="col-5">
          <p>Lorem ipsum dolor sit amet.</p>
        </div>
        <div class="col-2">
          <p>Lorem ipsum dolor sit amet.</p>
        </div>
      </div>
      <div class="row">
        <div class="col-6">
          <p>Lorem ipsum dolor sit amet.</p>
        </div>
        <div class="col-8">
          <p>Lorem ipsum dolor sit amet.</p>
        </div>
        <div class="col-4">
          <p>Lorem ipsum dolor sit amet.</p>
        </div>
      </div>
    </div>
```

# **Components**

Bootstrap components are the strong point of bootstrap as it has different components from dropdown menus to button groups to paginations and carousels and much more which you can easily use by just copying the component you like and paste it into your project.

Examples of bootstrap components:

1. [**Alerts**](https://getbootstrap.com/docs/5.1/components/alerts/)
2. [**Carousel**](https://getbootstrap.com/docs/5.1/components/carousel/)
3. [**Card**](https://getbootstrap.com/docs/5.1/components/card/)
4. [**Navbar**](https://getbootstrap.com/docs/5.1/components/navbar/)
5. [**Button group**](https://getbootstrap.com/docs/5.1/components/button-group/)
6. [**Pagination**](https://getbootstrap.com/docs/5.1/components/pagination/)

# **Pulse Check**

Build and customize a frontend page using bootstrap only, use at least two unmentioned components in your page, and make sure to use the grid layout.
