---
title: "React Redux Flux Pattern"
slug: react-redux-flux-pattern
---

# What is Flux?

Flux is an application architecture pattern used by Facebook for 
building client-side web applications. It utilizes a unidirectional
data flow to create predictable and reliable state changes. 

Flux is a pattern used to create frameworks or libraries. 
As such Flux is more concept than concrete code. 

Flux is language agnostic. You can implement Flux in any language. 

## What is Application State? 

Application state is the data your application manages and displays 
in various views.

## Flux 

Applications using Flux have three parts: 

- Dispatcher
- Store 
- View

Actions are sent to the Dispatcher which updates the Store. When the 
store is updated views are refreshed to display the changes. 

![01-unidirectional-data-flow](./assets/01-unidirectional-data-flow.png)

Actions can be sent from views. From there the system follows the same 
process. 

![02-actions](./assets/02-actions.png)

Data flows into views when the store is updated.

![03-views](./assets/03-views.png)

## Notes 

A key feature, and requirement of Flux is that data in the store is 
**immutable**. Data is replaced it is **never modified**.

For primitive values, Strings and Numbers, setting the value 
creates a new value.

For Objects and Arrays, which are refernece types updating the value 
of an Array doesn't create a new array it only mutates the original!
The same is true for setting the properties of objects. 

To understand why this is let's take a closer look at Objects, 
Object References, and Object Equality. 

## Equality

When updating the store it's important to assign a new value, rather 
than mutate the current value. 

With primitve types this is easily done and can be checked by comparison. 

**Example 1**

```JavaScript 
const state = 10;
const newState = 66;
console.log(state === newState); // false 
```

Old `state` and `newState` are not equal. This might seem obvious.
Look at the next few examples and you will see that it is 
not always obvious. 

**Example 2**

```JavaScript
const state = { value: 10 };
const newState = state;
newState.value = 66;
console.log(state === newState); // true
```

In this case not only are `state` and `newState` equal they are 
in fact the same object! 

`console.log(state.value); // 66`

The same is true for Arrays. Remember in JavaScript 
Arrays and Functions are Objects! 

**Example 3** 

```JavaScript
const state = ["A", "B", "C"];
const newState = state;
newState.push("D");
console.log(state === newState); // true
console.log(state); // ["A", "B", "C", "D"]
```

Again state and newState are the same Object!

**Example 5**

```JavaScript
const state = ["a", "B", "C"];
const newState = ["a", "B", "C"];
console.log(state === newState); // false
```

Variables assigned an Object or an Array hold a *reference* to that 
Object or Array.

In example 5 both arrays hold the same value but they are 
not equal! Each array references a different Array!

In example 5, we can see that creating two different Arrays 
creates two different references, that are not equivalent, 
even though the values stored in each reference are the same!

Study these ideas here: 

- https://repl.it/classroom/invite/STIb5DY

## Resources

- https://facebook.github.io/flux/docs/in-depth-overview.html#content
- https://blog.andrewray.me/flux-for-stupid-people/
- https://egghead.io/courses/getting-started-with-redux
