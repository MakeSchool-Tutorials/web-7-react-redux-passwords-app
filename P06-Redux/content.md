---
title: "React Redux - Redux"
slug: react-redux-redux
---

# Redux

Redux is a JavaScript implementation of the Flux pattern. 
Described as a Predicatable State Container for JavaScript 
Applications. 

Redux is a library written in JavaScript. 

## What does it do? 

Redux acts a central store for application state/data. You might not need 
it for many apps. In other apps it will solve problems that appear to be 
difficult. 

Wait what does Redux do again? Redux manages application state. That is Redux 
manages data that is share across your entire app. Beyond that is also 
manages changes to that data that make changes to data predictable and 
consistent. 

## Application State

Redux is a tool for managing application state. To understand when 
and where to use Redux necessitates an understanding of Application
State. 

Imagine Components as islands. Component state is like villages 
on islands. They can communicate with other villages on their island
but, have trouble communicating with people on other islands. 

Imagine Application state as a radio station. It allows you to send 
messages and share infomation with any village on any island anywhere 
in the ocean. 

If your islands are self contained and can run their life without 
connection to the outside world you don't need Redux. If, on the 
other hand, the villages (components) on islands throughout the ocean
(your app) need to communicate with other viallages using Redux 
will make this communication process easier to manage. 

Application state stored in Redux is easily shared across your entire
application. The component structure becomes irrelevant. 

Without Redux you will find that sharing data requires that state 
is owned and managed by a ancestor components. It is very difficult 
to pass data to components that are not descendants of component 
that owns the data. 

How does application state differ from Component State? Components
have their own state. Component state is stored in each component. 
Components can share state with child components. Sharing state 
with siblings or ancestors is more difficult.

### Some Examples 

So what's application state? Application state is the data your app 
stores, displays, and manages. Some examples are in order: 

- Twitter uses Redux. The state used by Twitter holds 
  - Tweets
  - settings
  - notifications
  - and much more...

See this article [here](https://medium.com/statuscode/dissecting-twitters-redux-store-d7280b62c6b1)

Basically anything displayed on your Twitter timeline, user profile, 
and all of the information used behind the scenes to control 
what is displayed is part of application state for Twitter. 

## Resources 

- https://redux.js.org
- https://egghead.io/courses/getting-started-with-redux