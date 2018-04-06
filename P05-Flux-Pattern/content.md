---
title: "React Redux Flux Pattern"
slug: react-redux-flux-pattern
---

# The Flux Pattern

Flux is an application architecture pattern used by Facebook for 
building client-side web applications. It utilizes a unidirectional
data flow. 

Flux is a pattern used to create frameworks or libraries. 
As such Flux is more concept than concrete code. 

Flux applications have three parts: 

- Dispatcher
- Store 
- View

Flux is similar to the MVC pattern but also different. Unlike MVC Flux imposes 
a **unidirectional** data Flow. When interaction occurs in a view an 
action is sent to the dispatcher which updates the store, and fianlly
data is passed to a views to update.  

Data can only flow one way. 

Actions must pass through the system before another action can be processed. 

One way data flow.

![01-unidirectional-data-flow](./01-unidirectional-data-flow.png)

Actions can be sent from views.

![02-actions](./02-actions.png)

Data flows into views when the store is updated.

![03-views](./03-views.png)

## Resources 

- https://facebook.github.io/flux/docs/in-depth-overview.html#content
