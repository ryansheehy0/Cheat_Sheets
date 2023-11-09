[Home](./README.md)

# Redux and Context
To prevent passing state all the way down to the children.
Used for managing global state.

Prop drilling.

Redux requires a lot of boilerplate code.

useContext hook

Actions: Plain JS obj that describes the changes you want to make to state

Reducer:
A big switch statement what switches based on the type
  - Don't change state, but returns state

Store:
Grants the entire application access to teh dispatch function and global state.

State Tree

global state
- 

Read Only

Dispatching actions changes the state tree

reducer(state, action)
curent state
actin

Don't use side effects in your reducer
- No global vars

Impure func
  - Each time you call it with the same args it might return something different

Redux is a react state library

createContext
provide it
use it

Use privide to use values in global state

Which component do we want to re-render when

UserContext is store

Provider is state managment

Reducers
Sometimes components can have a lot of states
