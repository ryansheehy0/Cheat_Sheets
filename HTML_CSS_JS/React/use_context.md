<!--
 * This file is part of RS Cheat Sheets.
 *
 * RS Cheat Sheets is free software: you can redistribute it and/or modify
 * it under the terms of the GNU General Public License as published by
 * the Free Software Foundation, either version 3 of the License, or
 * (at your option) any later version.
 *
 * RS Cheat Sheets is distributed in the hope that it will be useful,
 * but WITHOUT ANY WARRANTY; without even the implied warranty of
 * MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
 * GNU General Public License for more details.
 *
 * You should have received a copy of the GNU General Public License
 * along with RS Cheat Sheets. If not, see <https://www.gnu.org/licenses/>.
 */
-->

[Home](../../README.md)

# useContext
Context allows you to avoid manually passing props down at every level of your component tree.

Redux is both a library and a design patter.

If you have a button which when clicked changes another component you have to pass the button's state to that component. In order to do this, the button's state can no longer live in the button, but instead it has to live in the closes parent. This parent then passes the state to the button and the component you want to change when the button is clicked, this is called prop drilling. As an app grows in complexity, parent components end up having more and more state and things become more and more confusing.

The solution to this is having a global state which can be accessed by any component.

The Redux pattern involves 3 things:
- **Store**: Grants the entire application access to the dispatch function and global state.
- **Actions**: Plain JS Objects that describe the changes you want to make to the global state.
  - Actions have a type field(type of action) and a payload field(data that changes the state).
- **Reducer**: A big switch statement which takes in the current state and an action, switches based on the type of the action, and return a new new state with the payload on the action.

A **dispatch function** is used to trigger an action which is sent to the reducer.

The **state tree** is a JS Object that holds the entire state of your app.

When the button is clicked an action will be dispatched to the reducer. The reducer creates a new state based on the action.

Redux requires a lot of boilerplate code.

The store is immutable which makes it easier to debug. You know which components are modifying the store through dispatches.

If you were to throw an event when the button is clicked and add an event listener to the component you want to change when the button is clicked, then in a more complex application this can be very difficult to keep track of all your events and interactions between components.
  - With the redux design patter you don't need to worry about adding addEventLister s

## Table of Contents
<!-- TOC -->

- [useContext](#usecontext)
	- [Table of Contents](#table-of-contents)
	- [Questions](#questions)
	- [Installation](#installation)
	- [Context](#context)
		- [Creating a Context](#creating-a-context)
		- [Providing the context](#providing-the-context)
		- [Consuming the state from the provider](#consuming-the-state-from-the-provider)
		- [Redux patter with Context](#redux-patter-with-context)
			- [Actions](#actions)
			- [Reducers](#reducers)
			- [useReducer](#usereducer)
			- [Dispatching an action](#dispatching-an-action)

<!-- /TOC -->

## Questions

## [Installation](#table-of-contents)
`npm install @reduxjs/toolkit react-redux`

## [Context](#table-of-contents)
Context is built into React which allows you to share state globally across components without explicitly passing props. It follows the Redux design pattern.

- A **Provider** is a Context component that wraps children elements and allows them to share state and other information.
- A **Consumer** is a child of a provider and uses the state provided by that provider.
- A **Context** refers to the provider and any children components of that provider.

You can make a provider wrap around you whole application to allow for global state in your application

Instead of passing the state through each of the consumer's props you can instead directly use the state from the consumer itself.

### [Creating a Context](#table-of-contents)
The `value` attribute for a provider allows anything in it to be used by consumers.

In utils/UserContext.jsx

```javascript
import { createContext, useContext, useState } from 'react'

const UserContext = createContext()
export const useUserContext = () => useContext(UserContext) // Returns the value attribute in the provider

export default function UserProvider({children}){
  const [currentUser, setCurrentUser] = useState({
    name: 'John',
    role: 'Admin',
    id: 142323,
  })

  const variable = "You can also allow consumers to use variables."

  return (
    <UserContext.Provider value={ { currentUser, setCurrentUser, variable }}>
      {children}
    </UserContext.Provider>
  )
  // You could also just spread the props which will do the same thing as including the children. Make sure not to dereference props.
  return (
    <UserContext.Provider value={ { currentUser, setCurrentUser, variable }} {...props}>
  )
}
```

### [Providing the context](#table-of-contents)

In App.jsx

```javascript
import UserProvider from "./utils/UserContext"
import ChildComponent from "./components/ChildComponent"

export default App(){
  return (
    <UserProvider>
      <ChildComponent>
    </UserProvider>
  )
}
```

### [Consuming the state from the provider](#table-of-contents)

In ./components/ChildComponent.jsx

```javascript
import { useUserContext } from "../utils/UserContext"

export default function ChildComponent(){
  const { currentUser, setCurrentUser } = useUserContext()

  return (
    <div>
      <p>{currentUser.name}</p>
      <p>{currentUser.role}</p>
      <p>{currentUser.id}</p>
    </div>
  )
}
```

### [Redux patter with Context](#table-of-contents)

#### [Actions](#table-of-contents)
The utils/actions.js file is a small file tht lists the actions as strings and sets them for variables. This is only used to make autocompletion for your IDE easier.

In utils/actions.js

```javascript
export const TOGGLE_THEME = 'TOGGLE_THEME'
```

#### [Reducers](#table-of-contents)
Reducers provide a more organized way to change state in your application.

In utils/reducer.js

```javascript
import { TOGGLE_THEME } from './actions'

export const reducer = (state, action) => {
  // action includes type and payload
  const newDarkTheme = !state.darkTheme
  switch(action.type){
    case TOGGLE_THEME: {
      return {
        ...state,
        darkTheme: newDarkTheme,
      }
    }
    default:
      return state
  }
}
```

#### [useReducer](#table-of-contents)
The useReducer creates one large state object for you application. This large state object is called the state tree.

The state tree is modified in the reducer file.

In utils/ThemeContext.jsx

```javascript
import { createContext, useContext, useReducer } from 'react'
import { reducer } from './reducers' // Including your reducer file

export const ThemeContext = createContext()
export const useThemeContext = () => useContext(ThemeContext)

export default function ThemeProvider(props) {
  const initialState = { // Initial state of the state tree
    darkTheme: false
  }
  const [state, dispatch] = useReducer(reducer, initialState)

  return <ThemeContext.Provider value={[state, dispatch]} {...props} />
}
```

#### [Dispatching an action](#table-of-contents)

In a consumer component

```javascript
import { useThemeContext } from "../utils/ThemeContext"
import { TOGGLE_THEME } from "../utils/actions"

export default function Consumer(){
  const [state, dispatch] = useThemeContext()

  function toggleTheme(){
    dispatch({
      type: TOGGLE_THEME,
      payload: state.darkTheme // The reduce isn't using the payload so we don't really need it in this example
    })
  }

  return (
    <>
      <p>The theme is {state.darkTheme ? "dark theme." : "light theme"}</p>
      <button onClick={() => {toggleTheme()}}>Toggle Theme</button>
    </>
  )
}
```