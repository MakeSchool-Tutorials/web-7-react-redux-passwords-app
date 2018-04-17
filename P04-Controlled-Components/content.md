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
structure of the document in JavaScript. When changes occur in the virtual 
DOM React only edits the elements in the actual DOM that have changed. 
This is much faster than accessing elements in the DOM directly. 

Using the virtual DOM introduces some problems. For example if you create a 
reference to an element in the DOM there is no guarantee that the element 
will not be removed and replaced when the virtual DOM needs to make an 
update. 

This problem comes into play with form elements since these need to update their 
content often. 

## The Controlled Component Pattern

The Controlled Component Pattern keeps the value of the form element in state, 
sets the value via the element's onChange event, and sets the value of the 
element to value stored in state. This sounds more complicated than it is. 
Let's break it down: 

Imagine an example with an input field. 

1. When the value in the field is changed this triggers an `onChange` event. 
2. Use `onChange` to set a value on component state. 
3. Changes to state update the component. Setting the value of the input to the 
value in state syncs the component to display the value input. 

Try it out. Add the following to the `Password` Component. 

```JSX
<div>
  <input
    onChange={(e) => {this.setState({ password: e.target.value })}}
    value={this.state.password}
  />
</div>
```

This line sets the value for password on state when the input field changes. 

`onChange={(e) => {this.setState({ password: e.target.value })}}`

This line sets the value of the input when state changes. 

`value={this.state.password}`

This pattern works for most form elements. 

## Challenges 

Add another input that stores a name for the password. Remember you'll need to 
save the name on state. 

Use the input above in the Password component. This should allow you to generate 
a random password, type in your own choice of password, or modify the random 
password to make it more memorable. 

### Stretch Challenges

Add a checkbox under the input. This checkbox indicate whether we should add the 
hypens between each group of three characters or not. 

Use a select menu to choose one of three different password generators. 

- Letters
- Letters + Numbers
- Letters + Numbers + Punctuation

## Resources 

- https://reactjs.org/docs/forms.html#controlled-components
- 