---
title: "React Redux Implement React Redux"
slug: react--implement-redux-react-redux
---

# Implement React Redux

The following steps implement React Redux in a react project.

## Add Redux

Import redux into your project.

`npm i --save redux;`

This adds Redux as a dependency to the project.

There are a few more things we
to set up before we can implement Redux in React.

## Add react-redux

Add react-redux as a dependancy.

`npm i --save react-redux;`

Imagine this as the glue that binds Redux with React.

## Create Actions

Redux is very strict about how it allows state to be modified.
Changes to state can only be implement through actions which
you will define.

Create a folder named: 'src/actions'

Create a file in this folder: 'src/actions/index.js'

Imagine you want to store and manage passwords in your app.
The actions need to create new passwords, delete existing
passwords, and update existing passwords.

You will implement the store in a following step. The store
will be defined as an array and each password will
be stored at an index in that array.

Define these actions in 'src/actions/index.js'

```JavaScript
export const ADD_PASSWORD = "ADD_PASSWORD"
export const EDIT_PASSWORD = "EDIT_PASSWORD"
export const DELETE_PASSWORD = "DELETE_PASSWORD"
```

These are the action types. You need to export these so these
string constants can be shared throughout your code.

Next add some action creators.

```JavaScript
export const addPassword = (name, password) => {
  return {
    type: ADD_PASSWORD,
    payload: { name, password }
  }
}

export const deletePassword = (index) => {
  return {
    type: DELETE_PASSWORD,
    payload: { index }
  }
}

export const editPassword = (index, name, password) => {
  return {
    type: EDIT_PASSWORD,
    payload: { index, name, password }
  }
}
```

These functions are the action creators. These are simple functions
that return action objects.

Every action object has a type, which is set to an action type,
and a payload. Payload is a JS object with any properties.


## Define a Reducer function

Create a new folder: 'src/reducers'

Then add a new file to this folder: 'src/reducers/index.js'

Add another file: 'src/reducers/password-reducer.js'

In 'password-reducer.js' define a reducer function.

```JavaScript
import { ADD_PASSWORD, DELETE_PASSWORD, EDIT_PASSWORD } from '../actions'

const passwordReducer = (state = [], action) => {
  switch(action.type) {
    case ADD_PASSWORD:
      const { name, password } = action.payload
      return [...state, { name, password }]

    case DELETE_PASSWORD:
      const { index } = action.payload
      return [...state.slice(0, index), ...state.slice(index + 1)]

    case EDIT_PASSWORD:
      return state.map((item, index) => {
        if (index !== action.payload.index) {
          return item
        }
        return { ...item, ...action.payload }
      })

    default:
      return state
  }
}

export default passwordReducer
```

This block of code imports the Action Types.

It also defines the `passwordReducer` function.

This function is responsible for providing the default value for state.
The default state is defined here as the default value for the state
parameter.

`const passwordReducer = (state = [], action) => {...`

The switch statement in the function handles each action type.
Each case returns state. State is an array and when
state is modified rather modifying state each case returns a
**new copy of the array**.

This is a requirement for Redux! **Any changes to state must produce
new state!** You can not modify existing state.

## Combining Reducers

The store is a JavaScript object with properties that represent pieces
of application state. Each reducer is responsible for managing one
piece of state.

Add the following to 'src/reducers/index.js'

```JavaScript
import { combineReducers } from 'redux'
import passwordReducer from './password-reducer'

export default combineReducers({
  passwords: passwordReducer
})
```

This imports the `combineReducers` method from 'react-redux' and the
`passwordReducer` from 'src/reducers/password-reducer.js'

In this case the store will hold the array of passwords under the
key: 'passwords' and handle changes to this piece of state
with `passwordReducer`.

## Provider

Provider is a React Component that provides the Redux
store to it's child components. Provider is part of react-redux.

Add this at the top of App.js.

```JavaScript
import { createStore } from 'redux'
import { Provider } from 'react-redux'
```

Next import your reducers:

`import reducers from './reducers'`

Now create a store from your reducers:

`const store = createStore(reducers)`

Define the Provider for the App. This is a component that
should be an ancestor to components that want access to the Store.

```JSX
function App() {
  return (
    <Provider store={store}>
      <div className="App">
        <Password />
      </div>
    </Provider>
  );
}
```

At this stage you are implementing Redux and have defined a store. The
next step will be to connect components to the store.

## Password List

This a component that will list all of the passwords in the store.

Create a new component that will display a list of passwords. Create a new
file: 'src/password-list.js'.

```JSX
import React, { useState } from 'react'
import { connect, useSelector } from 'react-redux'

function PasswordList() {
  const passwords = useSelector((state) => state.passwords)

  const passwordList = passwords.map((pass, index) => {
    return (
      <div key={index}>
        name:{pass.name} password: {pass.password}
      </div>)
  })
  
  return (
    <div>
      {passwordList}
    </div>
  )
}

export default PasswordList
```

Here you imported `useSelector` from react-redux. You used this to get the list of passwords from the store with: 

```JS
const passwords = useSelector((state) => state.passwords)
```

The function passed to `useSelector()` takes state as a parameter and returns a value that you want from state. Here you returned `passwords` from state. 

## Save a Password

In this next section you will add code that will allow you to create and save new passwords to the list of passwords. 

## Add a name field

Currently the Password component generates a password we'd like to be able to add a password to a list of saved passwords.

Besides adding a password we'd also like to include a name with every password we save.

Open the Password Component. Edit the component to add a new value on state that will hold the name. 

Use a hook to keep track the value in the field:

```JavaScript
import React, { useState } from 'react'
```

Add a new value and setter for the name: 

```JS
const [name, setName] = useState('')
```

Add a new input field to show and edit this value. This should go above the password input in the render method. 

```JavaScript 
<input
  value={name}
  onChange={(e) => setName(e.target.value)}
/>
```

## Add password

Use the useDispatch hook. Import it at the top along with the action creator function addPassword. 

```JavaScript
import { useDispatch } from 'react-redux'
import { addPassword } from './actions'
```

Add a button that does this within the render method:

```JSX
<div>
  <button onClick={(e) => {
    const dispatch = useDispatch()
    dispatch(addPassword(name, password))
  }}>Save</button>
</div>
```

## Testing your work

Clicking the 'Save' button should add a new password to the list. Doing this
should display the name and password to the PasswordList.

## Resources

-
