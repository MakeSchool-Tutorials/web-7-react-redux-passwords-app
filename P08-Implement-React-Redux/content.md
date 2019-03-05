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
class App extends Component {
  render() {
    return (
      <Provider store={store}>
        <div className="App">
          <Password />
        </div>
      </Provider>
    );
  }
}
```

At this stage you are implementing Redux and have defined a store. The
next step will be to connect components to the store.

## React Containers

Containers are components that are connected to the Redux store. Container
Components recieve state in the form of props when the store is updated
and send actions to the dispatcher to trigger changes in state.

To create a Container you need to connect a component to Redux via the
`connect` method.

## Connect method

The connect method *connects* components to the redux store. To make this
work you will use two methods: `mapStateToProps` and `mapDispatchToProps`.

### mapStateToProps

The `mapStateToProps` method receives state from the Store and
returns an object containing values to be passed to your container/component
as props.

### mapDispatchToProps

The `mapDispatchToProps` method maps the action creator methods you defined
to props in your container/component.

## Add a name field

Currently the Password component generates a password we'd like to be able to add a password to a list of saved passwords. 

Besides adding a password we'd also like to include a name with every password we save. 

Open the Password Component. Edit the constructor to add a new value on state that will hold the name. 

```JavaScript
constructor(props) {
  super(props)
  this.state = { 
    password: 'p@ssw0rd', 
    name: 'My Password' 
  }
}
```

Add a new input field to show and edit this value. This should go above the password input in the render method. 

```JavaScript 
<input
  value={this.state.name}
  onChange={(e) => this.setState({ name: e.target.value })}
/>
```

## Turning the Password component into a container

Now it's time to connect this component to redux. 

Import connect from react-redux

`import { connect } from 'react-redux'`

We want to add a new password to do this we need to send a message to redux with an action from one of our action creators. Import the action creator at the top. 

`import { addPassword } from './actions/'`

Now it's time to connect this action to the reduc store. At the bottom of the class above the export statement add a method to map this method to the dispatcher: 

```JavaScript
const mapDispatchToProps = () => {
  return {
    addPassword
  }
}
```

Now replace the export statement at the bottom of the page with the following: 

`export default connect(undefined, mapDispatchToProps())(Password)`

The first parameter was not used used, but we needed to set the second parameter. 

Now we can use the addPassword but we will call it from props. Add a save button. Put this in the render method at the bottom. 

```JavaScript
<div>
  <button onClick={(e) => {
      this.props.addPassword(this.state.name, this.state.password)
    }}>
    Save
  </button>
</div>
```

Here you are calling addPasswrd from this.props and the name and password from state. 

## Password List

This a component that will list all of the passwords in the store.

Create a new component that will display a list of passwords. Create a new
file: 'src/password-list.js'.

```JSX
import React, { Component } from 'react'
import { connect } from 'react-redux'

class PasswordList extends Component {

  getList() {
    return this.props.passwords.map((pass, index) => {
      return (
        <div key={index}>
          name:{pass.name} password: {pass.password}
        </div>)
    })
  }

  render() {
    return (
      <div>
        {this.getList()}
      </div>
    )
  }
}

const mapStateToProps = (state) => {
  return {
    passwords: state.passwords
  }
}

export default connect(mapStateToProps)(PasswordList)
```

This is the minimal needed to display a list of passwords with their names.

The list of passwords is generated from the array of passwords in the redux store.
This is passed through `mapStateToProps` to `this.props.passwords` the component.
The last line `export default connect(mapStateToProps)(PasswordList)` makes this
possible.

Notice, the last line is the default export, instead of exporting the class as
usual.

At this point there are no passwords in the list, so nothing is displayed. You
need to add passwords to the list.

Modify `src/password.js` Password component. This component was not initially
set as a container/component. You need to convert this component into a
container.

Import `connect` from 'react-redux' and `addPassword` from '../actions' at the
top of the class.

```JavaScript
import { connect } from 'react-redux'
import { addPassword } from './actions'
```

Add `mapStateToProps` and `addDispatchToProps` at the bottom of the module.

```JavaScript
const mapStateToProps = (state) => {
  return {

  }
}

const mapDispatchToProps = () => {
  return {
    addPassword
  }
}
```

Last use `connect` to connect this component to Redux.

Replace `export default Password` with:

```JavaScript
export default connect(mapStateToProps, mapDispatchToProps())(Password)
```

Last, you want to save a password by calling the action creator: `addPassword`
with the name and password.

Add a button that does this within the render method:

```JSX
<div>
  <button onClick={(e) => {
    this.props.addPassword(this.state.name, this.state.password)
  }}>Save</button>
</div>
```

## Testing your work

Clicking the 'Save' button should add a new password to the list. Doing this
should display the name and password to the PasswordList.

## Resources

-
