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

Redux implements the Flux pattern in your JavaScript Applications. 

Redux acts as a central store for application state/data.

Redux stores the data your application works with. It also manages
changes to that data that keep the changes predictable and 
reliable. 

Redux/Flux is a tool for managing application state. There are 
two features of this that effect how your applications functions. 

First sharing state across components can become complicated 
as the structure of components becomes complex. redux makes 
sharing data between components easier since the store is 
contained in a single place. 

Second, Redux/Flux makes changes to application state more 
reliable. All changes to state must be happen through an 
action, and changes to state must be completed before the 
next action is applied.

## Application State

Application state is any data that your application stores and manages. 
This could be names and numbers in an andress book, any objects that 
are displayed and managed by the app. Data loaded from a web API. 

### Some Examples 

The Twitter web site uses React and Redux. 

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
- https://medium.com/@cabot_solutions/flux-the-react-js-application-architecture-a-comprehensive-study-fd2585d06483
