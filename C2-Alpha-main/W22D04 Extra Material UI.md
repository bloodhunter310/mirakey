# **Material UI**

**High-Level Goals**

By the end of this lesson, you will be familiar with the following:

- What is Material UI
- Installation
- Importing Components
- Using Material UI icons
- Using makeStyles
- Grid System and Container

# **What is Material UI**

Frontend library for react applications that allows you to import and use different components to create a user interface, it has a lot of components so you don&#39;t have to build everything from scratch which makes it easy to use.

# **Installation**

There are two ways to install and use Material UI on your project:

To install it and save it in your package.json dependencies through npm, this is recommended to use Material UI.

Use this command to add it to your application:


```
npm install @material-ui/core
```
Once it is installed check your package.json file to make sure it is added.

# **Importing Components**

To use Material UI components just add

Import name-of-component from &quot; @material-ui/core/name-of-component&quot;

For example
```
 import Button from "@material-ui/core/Button"
```

then you can call this component and use it using tags

```html 
<Button>Click</Button>
```

To customize the imported components you can use Material UI parameters such as variant and color, click [this link](https://material-ui.com/components/buttons/) for further reading, also make sure to check other components as well.

You can also apply your own style to customize any Material UI component by adding the style prop to your component.

```html 
<Button  style={{
       color:'red'
        }}
          >
        Click</Button>
```

It&#39;s preferable to use the already existing Material UI props, but do know that you can always add your own styles.

# **Using Material UI icons**

To start using icons first use this command to add it to your application:

```
npm install @material-ui/icons
```

To use Material icons just add

```
import HomeIcon from "@material-ui/icons/Home"
```

For example importHomeIconfrom&quot;@material-ui/icons/Home&quot;

then you can call this icon and use it using tags

```html 
<HomeIcon />
```

You can also add icons to the components using startIcon and endIcon prop for example

```html 
  <Button 
      startIcon={<HomeIcon />}
      endIcon={<HomeIcon />}
          >
        Click</Button>
```

Use [this link](https://material-ui.com/components/icons/) for further reading of Material UI icons.

# **Using makeStyles**

We can create a constant variable called useStyles and call makeStyles inside this constant we pass a root style so we can apply it to our components, this will work and be used as a CSS classes to reduce the redundancy of the written styles and can be easily based to any component you want using className.

For Example:

```html 
import Button from "@material-ui/core/Button"
 
 
import { makeStyles } from '@material-ui/core';
 
const useStyles = makeStyles({
  root:{
    borderRadius:20,
    border:5,
  }
})
 
function FirstStyle(){
  const classes = useStyles();
  return <Button variant="contained" color="primary" className={classes.root} >Click</Button>
}
 
function App() {
  return (
    <div className="App">
<FirstStyle />
    </div>
  );
}
 
export default App;
```

# **Grid system and Container**

Import and place the Container at the top level so it can wrap every component you have in the application, the container represents a max-width in your page and holds each component inside of it. Pass a max-width prop to control the container width.

Check [this link](https://material-ui.com/components/container/) for further reading.

The grid system is a 12 column system, to use it we have to use what&#39;s called a grid container it defines what you want to wrap inside your grid and you use it by passing a container prop inside the grid tag, then we use grid item which specifies the components inside the grid and you use it by passing an item prop inside the grid tag.

The grid will place the components next to each other, so you need to specify how many columns you want each grid item to take using media query sizes to specify at what size you want it to take a number of columns, then the number of columns.

For example:

```html 
   <Grid container>
        <Grid item md={3}>
          <Button variant="contained" color="primary">
            Click
          </Button>
        </Grid>
        <Grid item md={3}>
          <Button variant="contained" color="secondary">
            Click
          </Button>
        </Grid>
        <Grid item md={3}>
          <Button variant="contained" color="link">
            Click
          </Button>
        </Grid>
        <Grid item md={3}>
          <Button variant="contained" color="default">
            Click
          </Button>
        </Grid>
      </Grid>

```

# **Pulse Check**

Build and customize a React page using Material UI only, use at least two unmentioned components in your page, and make sure to use the grid system.
