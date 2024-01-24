[Home](../README.md)

# React hooks
React hooks allow functional components to manage state, handle lifecycle events, and perform side effects.

| Hook name       | Description                                                      |
|-----------------|------------------------------------------------------------------|
| useState        | Manages state in functional components                           |
| useEffect       | Performs side effects in functional components                   |
| useContext      | A child in a context can access any variable in that context     |
| useReducer      | Manages complex state logic using a reducer function             |
| useRef          | Creates a mutable object references that persists across renders |
| useCallback     | Stores callback functions to prevent unnecessary re-renders      |
| useMemo         | Stores values to prevent unnecessary computations. Like caching  |
| useEffectEvent  | Listens to custom events using useEffect                         |
| useLayoutEffect | Like useEffect, but fires synchronously after all DOM mutations. |
| useTransition   | Enables multiple components to render at the same time           |

Not frequently used so maybe not put in
| Hook name           | Description                                                     |
|---------------------|-----------------------------------------------------------------|
| useDifferedValue    | Delays the rendering of an asynchronous value until it's needed |
| useImperativeHandle | Customizes the instance value that is exposed by forwardRef     |
| useDebugValue       | Customizes label displayed for custom hooks in react dev tools  |
| useId               | Generates a unique identifier for a component instance          |
| use()               |                                                                 |
| useFormStatus       |                                                                 |
| useOptimistic       |                                                                 |

## Table of Contents

<!-- TOC -->

- [React hooks](#react-hooks)
	- [Table of Contents](#table-of-contents)
	- [Custom hooks](#custom-hooks)
	- [useState](#usestate)
	- [useEffect](#useeffect)
	- [useRef](#useref)
		- [React.forwardRef](#reactforwardref)
	- [useMemo](#usememo)

<!-- /TOC -->

## [Custom hooks](#table-of-contents)


## [useState](#table-of-contents)
State is used for variables that when changed should cause a re-render on the screen. These tend to be variables that are different for each client who visits the site.

`useState` tells React that something has changed so react can re-render the DOM.

In react when a page is re-rendered(because of a state change) then the component function is ran again to return the JSX.

```javascript
import { useState } from 'react'

export default function Counter() {
  // Array destructing
  const [count, setCount] = useState(0/*Initial value of state*/)
    // count is the value of the state at that moment. Get variable
    // setCount is used to update the state. Set method

  const handleClick = () => {
		// If you are using the set method with the previous value of the state then it is recommended to use
		setCount((count) => count + 1) // This ensures that the count state is up to date

		// If you are just setting the state you can use
		setCount(2)

		// You cannot do because it won't tell react to re-render
    count += 1

		// The set method takes time to update the state
    console.log(`New value of count: ${count}`) // Previous value of count because setCount hasn't had time to update count
  }

  return (
		<>
			<button onClick={handleClick}>+</button>
			<p>Click count: {count}</p>
		</>
	)
}
```

## [useEffect](#table-of-contents)
useEffect is used to run code based upon some variable changing or upon the component rendering.

useEffect is often used for things in the app that need to interact with the external world like API requests, localstorage, etc. These are called sideEffects.

useEffect never returns anything

```javascript
import {useEffect, useState, useRef} from "react"

const Component = () => {
	const [state1, setState1] = useState(true)
	const [state2, setState2] = useState(true)

	useEffect(() => {
		// Only run when mounted/on first load of app
	}, [])

	useEffect(() => {
		// This code is ran on every DOM re-render
	})

	useEffect(() => {
		// When the state changes this code is ran. Not ran on initial load.
	}, [state1])

	useEffect(() => {
		// When the state1 or state2 changes this code is ran
	}, [state1, state2])

	const variable = "Initialized variable"
	useEffect(() => {
		// This will run on initial render because variable was originally un-initialized and then it became initialized which is a change.
	}, [variable])
}

export default Component
```

Why does useEffect [] run twice on reload when useStrick is being used on your react app.

## [useRef](#table-of-contents)
When a reference is changed it doesn't cause your component to re-render.

### [React.forwardRef](#table-of-contents)
React forward ref on a component allows you to use ref as a function in a parent component. This is useful for creating an array of refs in the parent component.

```javascript
const Component = React.forwardRef(props, refs) => {
}

export default Component

// In parent component
const componentRefs = useRef([])
return (
  <Component
    ref={(ref) => {componentRefs.push(ref)}}
  />
)
```

## [useMemo](#table-of-contents)
When you have slow functions that don't need to be called frequently you can useMemo in order to store the value.

It is not recommended to use useMemo when it isn't needed because it will take up more memory and decrease performance.

```javascript
import { useState, useMemo } from 'react'

const Component = () => {
	const [number, setNumber] = useState(0)
	const var = useMemo(() => {
		return slowFunction(number)
	}, [/*Dependencies*/number])
	// Whenever the dependency changes then teh slow function is ran.
	const var = slowFunction(number) // This will run every render which will cause performance problems.

	return ()
}
export default Component
```

If you are returning an object and you want the reference to that object not to change you can also use useMemo.