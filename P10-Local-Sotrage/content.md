---
title: "React Redux Local Storage"
slug: react-redux-local-storage
---

# Local Storage

At this stage your app should keep track of passwords but the list is 
lost when then app is refreshed. The goal is save the password data 
locally so it can be retrieved and displayed again. 

Local Storage is a browser feature that allows apps to store data 
locally. What does that mean? 

Local storage stores data locally. Data is saved with browser on the 
device. 

Local starage saves data as a key and value pair. Values are limited 
to strings or anything that can be converted to a string. This works
well with JSON. 

## `localStorage`

`localStorage` has two methods `getItem` and `setItem`. The first
retrieves data saved to localstorage, the second saves data to 
the local store. 

### `setItem`

Set an item with a key: 

`localStorage.setItem('key', 'some value')`

### `getItem`

Get the value stored with the key: 

`localStorage.getItem('key')`

## `JSON.parse` and `JSON.stringify`

Values saved to local storage must be strings or numbers. 
JavaScript Objects and Arrays can be converted to Strings in JSON 
format. Which makes these a very convenient format for local storage. 

You can convert an Object or Array to a JSON string with 

`JSON.stringify(obj)`

and parse a JSON back into a JavaScript object or array with: 

`JSON.parse(json)`



## Add local storage to the app

Add the following to 'App.js' or put it in another file and import the 
the two methods to 'App.js'. If these emthods are added to 'App.js' 
they need to be defined before: `const store = createStore(...)`.

```JavaScript
const PSSWRDZ_STATE = "PSSWRDZ_STATE"

// Load State
export const loadState = () => {
  try {
    const serializedState = localStorage.getItem(PSSWRDZ_STATE)
    if (serializedState === null) {
      return undefined
    }
    return JSON.parse(serializedState)
  } catch(err) {
    return undefined
  }
}

// Save State
export const saveState = (state) => {
  try {
    const serializedState = JSON.stringify(state)
    localStorage.setItem(PSSWRDZ_STATE, serializedState)
  } catch(err) {
    console.log("Error saving data:"+err)
  }
}
```

The first method loads state from the key defined on line 1. 
If there is nothing stored for that key it returns undefined. 

The second method takes `state` as a parameter serializes this 
into a JSON string and saves that to local storage with the 
key defined on line 1. Here we `try` the operation and catch
any errors that occur. 

With these two methods in place you can save retrieve data. 

Since the Redux store is a JavaScript object you can pass it 
`saveState` and save it with local storage. 

## Access the Store and Dispatcher

Replace `const store = createStore(reducers)` with: 

```JavaScript
const persistedState = loadState()
const store = createStore(reducers, persistedState)
store.subscribe(() => {
  saveState(store.getState())
})
```

There are three operations in the code above. 

First, the sotre is loaded from local storage by calling
`loadState()`. THis should return an Object or `undefined`.

The second line creates a new Redux store. The second 
parameter allows us to create a store from an existing 
object. This prepopulates the store with data. 

The last line subscribes to the store for updates. The 
function passed to the `subscribe` method will be called 
each time the store is updated. This means the calls we 
make to 

## Resouces 

- 