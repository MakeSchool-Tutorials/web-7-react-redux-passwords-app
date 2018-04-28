---
title: "React Redux Styling the Project"
slug: react-redux-styling-the-project
---

# Styling the Project

CSS is incredibly flexible. With a few lines of code you 
can describe the appearance of any object on the screen.

React's component structure offers different strategies 
for implementing CSS. 

Beyond React, the Create React App boilerplate also adds 
still more options for CSS. 

## Strategies

### Traditional Stylesheets

Stylesheet, like traditional web pages React apps can 
use a stylesheet with class tag names, class names, ids,
etc. 

Just make a style stylesheet and link to it in your base
document. In Create React App includes `index.css` you 
can put all of your styles here. 

**Pros**

Easy, all of your styles are in one place. 
Easy to share styles across elements. 

**Cons**

Not portable, it's difficult to move these styles to 
another project.

Styles for components are mixed with entire stylesheet. 
This could make it hard to edit or share move these 
to another project. 

### Import Styles

Create React App uses Webpack for preprocessing. One of
the built in preprocessing scripts converts CSS files 
imported into Components to style tags in the head of 
the document. 

This means you can import a CSS file into any Component 
and the styles will magically appear in the head of the 
document. The advantage to this is this allows your 
components to become portable. 

**Pros**

Components are portable. Styles and component files 
can be grouped together and moved from one project 
to another. 

**Cons**

Requires the Webpack be set up to handle this. 

### Inline Styles

While inline styles are generally shunned in 
traditional web dev. With React they make more 
sense. 

Inline styles are written into component files 
as JavaScript and assigned to elements with the 
style tag. 

**Pros**

Very portable, styles are written into the file 
where they are used. 

Styles can be calculated via JavaScript. This allows 
intersting options not available to regular CSS. 

**Cons**

Adding styles to your component files tend to make 
thos files larger and more code heavy. 

Inline styles Aren't shared so you'll end up with 
more source code, and code that is less DRY. 

## Examples 

These examples will all take style a button. We 
will take style the same button with the same 
styles. 

### Traditional Stylesheet

Give the button in your Component the class name
'button'. 

**Note! use the 'className' in place of 'class' 
in react Components. 

```jsx
<button 
  className='button'
  ...
>Generate</button>
```

In 'index.css' just style the 'button' class!

```css
.button {
  width: 100%;
  margin: 0.5em 0;
  padding: 0.5em;
  border: 4px solid #4687D3;
  border-radius: 6px;
  background: #4A90E2;
  color: #fff;
}
```

Done! That was easy. Realize that you will 
need to dig through this stylesheet to change 
the style for this button, it will buried in 
amongst all of the other styles you write. 

If you were to move this component to another
project you will need to extract these styles 
and move them into the new project.

### Import StyleSheet

In this case you will make a new stylesheet that 
will be imported into a component. It's a good 
idea to name this with the name of the component. 

Make a new file: 'src/password.css'

Add the styles here: 

```css
.button {
  width: 100%;
  margin: 0.5em 0;
  padding: 0.5em;
  border: 4px solid #4687D3;
  border-radius: 6px;
  background: #4A90E2;
  color: #fff;
}
```

Import this stylesheet into 'password.js'. 

```JavaScript
import './password.css';
```

Nice! Imagine if you arranged your files like 
this: 

```
- src
  - components
    - password
      - password.css
      - password.js
```

With this arrangement you can move the password 
component complete with it's styles by moving 
the folder!

**Important! This only works with the correct
webpack configuration!**

### Inline styles 

The last strategy is to use inline styles. 
The idea is to create a JavaScript Object 
containing the CSS properties and values, 
assigning this to the style property of a
react component. Try it for youself. 

In file 'src/password.js', not in the class. 
Define an Object to hold the style properties. 

```JavaScript
const styles = {
  button: {
    width: '100%',
    margin:'0.5em 0',
    padding: '0.5em',
    border: '4px solid #4687D3',
    borderRadius: '6px',
    background: '#4A90E2',
    color: '#fff'
  }
}
```

Put the button styles on the key 'button'. This 
way you can add other styles to other keys that 
will be applied to other elements. The key acts 
like the class name. 

Notice the property names are similar to the
CSS property names. Notice 'border-radius' is 
'borderRadius' here. 

All CSS properties have a JavaScript equivelent. 
The javaScript version of a CSS property is the
CSS name in camel case. 

Assign these styles to button. 

```JSX
<button
  style={styles.button}
  ...
  }}>Save</button>
```

Should work the same as the previous two examples. 

## Resources 

- 









