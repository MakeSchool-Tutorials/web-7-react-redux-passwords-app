---
title: "React Redux Controlled Components"
slug: react-redux-controlled-components
---

# What is a controlled Component? 

Controlled Component is a name used to describe form elements 
in React. Form elements require a special treatment due to the 
virtual DOM. 

## The virtual DOM

The DOM is Document Object Model, it is the structure of nodes or elements 
created from the an HTML document. 

Traversing and modifying elements in the DOM, like updating the text/html
content of a tag is a slow operation in the browser. 

React solves this speed issue by creating a virtual DOM that holds the 
structure of the document in JavaScript. Changes to the virtual DOM are
much faster than making changes to DOM directly. 

When the DOM needs to be changed the React uses a diffing algorithm to 
identify which elements need to be changed, and applies changes to only 
those elements in the DOM. 

Using the virtual DOM introduces some problems. For example if you create a 
reference to an element in the DOM there is no guarantee that the element 
will not be removed and replaced when the virtual DOM needs to make an 
update. 

## The Controlled Component Pattern

The Controlled Component Pattern keeps the value of the form element in 
*component state*. The value in state is set via the *form element's* onChange event.
The value of the form element is set to a value on the component's state. 
This sounds more complicated than it is. Let's break it down: 

Imagine an example with an input element (input tag). 

1. When the value in the input element is changed this triggers an `onChange` event. 
2. `onChange` handler sets a value in state on the component. 
3. Changes to state trigger the component to render. 
4. When the component renders, the value on state is set as the value of the input element. 

Try it out. Add the following to the `Password` Component. 

```JSX
<div>
  <input
    onChange={(e) => setPassword(e.target.value)}}
    value={password}
  />
</div>
```

This line sets the value of password *on state* when the input element changes. 

`onChange={(e) => setPassword(e.target.value)}}`

This line sets the value of the *input* when state changes. 

`value={password}`

This pattern works for most form elements. That inlcudes, checkbox, radio, 
select, textarea etc. 

## Challenges 

**Challenge 1**

Modify the Password component so the password displays in a text input. 
use the Controlled Component Pattern. 

**Challenge 2**

Add a new text input. This will be used to store a name or description for
the password. You will need to create another text input, and add another 
property to state. Use the Controlled Component Pattern again.

### Stretch Challenges

**Stretch Challenge 1**
Add a check box that indicates whether the password generated should 
contain hyphens between every 3rd character. e.g.

"6N1-kMH-d?i"

Hyphens should appear when the box is checked. And not when the box is
unchecked e.g.

"6N1kMHd?i"

Use the Controlled Component Pattern again with the check box. 

**Stretch Challenge 2**
Use a select menu to choose one of three different password generators. 

You can use one of these patterns, or make up your own. 

- Letters (Only letters: AbC...)
- Letters + Numbers (Letters and numbers: a2B...)
- Letters + Numbers + Punctuation (Letter, numbers, and punctuation: a2#...)

Use the Controlled Component Pattern again withe select element. 

You will need to modify your password generation code to handle the 
system chosen from the menu. 

## Resources 

- https://reactjs.org/docs/forms.html#controlled-components



