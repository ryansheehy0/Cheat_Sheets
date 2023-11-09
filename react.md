[Home](./README.md)

# React
A javascript UI framework that makes creating single page applications easier.

Why use react over vanilla JS:
- Easier to have JS work with the html directly
  - Don't need to querySelector, getElementById, etc all the time
  - React allows the state and UI to be combined.
- Html components which allows for reuse of html and/or having more abstraction
- Virtual DOM to increase performance
  - Without the virtual DOM the page will need to be repainted, css recalculated, update the layout, etc when the DOM changes.
  - Updates are bundled as to not repaint the page too much
  - React is very efficient for very complex UIs, but tends to be less efficient for apps where the DOM isn't being updated as much.


## Table of Contents

<!-- TOC -->

- [React](#react)
  - [Table of Contents](#table-of-contents)
  - [Questions:](#questions)
  - [Single Page vs Multi Page Apps](#single-page-vs-multi-page-apps)
  - [Virtual DOM](#virtual-dom)
  - [JavaScript XMLJSX](#javascript-xmljsx)
    - [Fragments](#fragments)
  - [Vite](#vite)
  - [File Structure](#file-structure)
  - [Components](#components)
    - [CSS in Components](#css-in-components)
    - [Props](#props)
      - [Props as embedded children](#props-as-embedded-children)
  - [Conditional Rendering](#conditional-rendering)
    - [React Router](#react-router)
      - [useParams](#useparams)
  - [Map function in React](#map-function-in-react)
  - [Event handling in React](#event-handling-in-react)
  - [Tailwind in React](#tailwind-in-react)
    - [Changing Tailwind with State](#changing-tailwind-with-state)
  - [useState](#usestate)
  - [Forms in React](#forms-in-react)
  - [useEffect](#useeffect)
  - [useRef](#useref)
  - [Testing in React](#testing-in-react)

<!-- /TOC -->

## Questions:
  - Hooks
    - State and other react features without writing classes. Can put them in functions.
    - Don't need this.setState
    - All hooks start with the word use
      - useState
      - useContext
      - Creating your own hooks
      - useRef
      - useParams
  - Short circuit operators
  - Where to put assets. Public or src/assets
  - Finish reserved attributes
  - What does `react-dom` do?
  - What is props.children
  - Do states re-run variables if they are set inside of the react function?

  Higher order component: Wraps the whole app to allow for functionality

  - Explain and use providers inside a React component.
  - Explain the concept of Consumer and accessing React Context.
  - Explain and use actions with a reducer function.
  - Explain reducers and use them with the useReducer Hook.

## [Single Page vs Multi Page Apps](#table-of-contents)
**Single Page Apps(SPAs)** are apps where page changes are handled by javascript and don't require a full page reload.

**Multi Page Apps(MPAs)** are apps where each page is a different html file which requires a reload to change between pages.

## [Virtual DOM](#table-of-contents)
The Virtual DOM is an object in memory that represents the real DOM.

When the virtual DOM is synced with the DOM it is called reconciliation.
- When you change the DOM in react the virtual DOM is changed
- The virtual DOM is compared with the old virtual DOM
- These differences are then batched/bundled to decrease the DOM from repainting the page too much
- React then updates the DOM with the batched differences

## [JavaScript XML(JSX)](#table-of-contents)
JSX allows you to write html like code in JavaScript.

You can use normal html elements and component elements inside JSX. Component elements always start with capital letters while html elements start with lowercase letters.

You can use JavaScript inside JSX with {}s. Whatever the js in the {}s returns, is converted into a string, including arrays, so it can be embedded in the JSX.

```javascript
const name = "ryan"
const jsx = <h1>Hello, {name}</h1>
{/*These are comments in JSX*/}
```

Every tag needs to be closed or self closed with </>s or />. Can't have non closed tags like in html like `<hr>`.

Instead of using the `class` attribute in html use the `className` attribute instead. This is to prevent any conflicts with the class keyword in JS.

### [Fragments](#table-of-contents)
Fragments are empty tags <></> that go around all the JSX components.

Functions can only return 1 value. The fragments allow you to return multiple component values as 1 single value to allow it to be returned.

## [Vite](#table-of-contents)
Vite is the build tool for react
- Fast Development Server
- On Demand compilation
- Hot reloading(Doesn't work for errors)
- Fast cold start
- Support pre-processors. Typescript

Initializes a new project using the vite framework
`npm create vite@latest` gets the latest version of vite

To run vite `npx vite`

Vite's default port is 5173.

vite.config.js

```javascript
import { defineConfig } from "vite"
import react from "@vitejs/plugin-react"

export default defineCOnfig({
  plugins: [react()],
  server: {
    port: 3000,
    open: true, // Open page when server starts
  }
})
```

If you do `npx vite --host` allows you to view your React app on mobile as long as you allow port forwarding. In the terminal the location should look like this: `Network: http://...`

## [File Structure](#table-of-contents)

```
public
src // Do reacted development
  assets
  components
    Component.jsx
  App.css // App specific css
  App.jsx // Imports App.css and is the start of app
  index.css // Takes president over App.css
  main.jsx // Imports react, app, index.css and renders App.jsx in the id root
index.html // React inserts into <div id="root"></div> and loads main.jsx
```

main.jsx

## [Components](#table-of-contents)
Each component tends to go in its own file.

```javascript
function HelloReact(){
  const text = "some text"

  return <h2>Hello World! Here is {text}</h2>
  // If you want to return with multiple lines
  return (
    <h2>
      Hello Word! Here is {text}.
    </h2>
  )
}

export default HelloReact
```

### [CSS in Components](#table-of-contents)

```javascript
// You can also set the className to style in css or put the css in the component itself
// CSS properties are in camel case
const styles = {
  card: {
    margin: 20,
    background: '#e8eaf6',
  },
  heading: {
    background: '#3f51b5',
    minHeight: 50, // pixels. Default unit is pixels
    fontSize: '1.2rem',
  },
};

function Card() {
  return (
    <div style={styles.card}>
      <div style={styles.heading}>Lorem ipsum dolor</div>
    </div>
  );
}

export default Card;
```

### [Props](#table-of-contents)
Props are arguments into react components.

Data in the parent components is passed to the child component through arguments/props.

Component.jsx

```javascript
function Alert(props) {
  return (
    <div className={`alert alert-${props.type || 'success'}`} role="alert">
      {props.message}
    </div>
  );
}

// You can also destructure props in the argument
function Alert({type, message}) {
  return (
    <div className={`alert alert-${type || 'success'}`} role="alert">
      {message}
    </div>
  );
}

export default Alert;
```

In parent component/App.js

```javascript
import Alert from './components/Alert';

const message = 'Invalid user id or password';
const alertType = "danger"

function App() {
  return <Alert type={alertType} message={message} />;
}

export default App;
```

Only non attribute JSX keywords are added to props.
- Ex: style won't be added.

| Reserved attribute             | Description                                          |
|--------------------------------|------------------------------------------------------|
| key                            | List item UUID so react knows which element is which |
| ref                            |                                                      |
| children                       |                                                      |
| dangerouslySetInnerHTML        |                                                      |
| defaultValue                   |                                                      |
| defaultChecked                 |                                                      |
| suppressContentEditableWarning |                                                      |
| suppressHydrationWarning       |                                                      |
| className                      |                                                      |
| class                          |                                                      |
| style                          |                                                      |
| onClick                        |                                                      |

Attributes can be set with {}s or ""s
  - `className={/*JavaScript*/}`
  - `className="string"`

#### [Props as embedded children](#table-of-contents)
React allows you to pass JSX as an embedded argument into components and which can be used with `props.children`

```javascript
return (
  <Component>
    <div>This is embedded JSX</div>
  </Component>
)

// Inside Component
export default function Component(props){
  return (
    <div>
      {props.children} {/* This will render <div>This is embedded JSX</div> in this example*/}
    </div>
  )
}
```

## [Conditional Rendering](#table-of-contents)
Since you can't put if statements in JSX you have to use ternary operators

```javascript
  // Not recommended to use. JSX might put in the literal value of "false"
  {props.message &&
   <div>Some JSX</div>
  }

 // It is recommended to do
 {props.message ? <div>Some JSX</div> : null}

 // Usually conditional rendering is done with states
 {state ? (
    <div>True</div>
  ) : (
    <div>False</div>
  )}
```

### [React Router](#table-of-contents)
Conditionally render content based upon what's in the url filepath.

Ex:
  `https://yoururl.com/filepath` where the pathname is /filepath

`npm install react-router-dom --save-dev`

| Components   | Description                                                                                                              |
|--------------|--------------------------------------------------------------------------------------------------------------------------|
| BrowseRouter | Allows other react router dom components inside of it                                                                    |
| Router       | Conditionally renders a component based on the current pathname                                                          |
| Routes       | Renders the first Router or Redirect that matches the current location                                                   |
| Link         | Link to another filepath that is handled by client side. <a/> is handled by server side which is what we don't want here |
| NavLink      | Same as Link component, but allows for additional styling with it's "to" prop if the path is the current pathname        |
| Redirect     | Redirects the filepath from something to something else                                                                  |

```javascript
import React from "react"
import { BrowserRouter as Router, Route, Routes, Link, Redirect } from "react-router-dom"
import Home from './components/Home';
import About from './components/About';
import Contact from './components/Contact';
import NotFound from './components/NotFound';

export default function Routes(){
  return (
    <Router>
      <Routes>
        <Route path="/" exact><Home /></Route> {/*If the path is exactly /*/}
        <Route path="/about"><About /></Route> {/*Any pathname that starts with /about */}
        <Route path="/contact"><Contact /></Route>
        <Route path="/404"><NotFound /></Route>
        <Route> {/* If no path is specified then it is the default filepath*/}
          <Redirect to="/404" />
        </Route>
      </Routes>
      <Link to="/">Home</Link>
      <Redirect from="/old-path" to="/new-path" />
    </Router>
  )
}
```

| Hooks         | Description                                       |
|---------------|---------------------------------------------------|
| useHistory    |                                                   |
| useLocation   | A hook that returns the current location/pathname |
| useParams     | Get the parameters of the url                     |
| useRouteMatch |                                                   |

#### [useParams](#table-of-contents)

```javascript
// Example path: /user/:id
import { useParams } from "react-router-dom"

export default User(){
  const { id } = useParams
  return <p>id</p>
}

// useParams can also handle multiple parameters
// Example path: /user/:username/:id
export default User(){
  const { username, id } = useParams
  return <p>id</p>
}
```

## [Map function in React](#table-of-contents)
Map in react allows you to render more than 1 of the same element.

Since map returns an array it gets converted. forEach doesn't return anything so it won't work.

```javascript
// Items is an array of objects being mapped over
return (
  <ul>
    {items.map(item => (
      <li key={item.uuid}>
        {item.value}
      </li>
    ))}
  </ul>
)
```

Each child in a list should have a unique key attribute. React uses this to know which list item is which.

## [Event handling in React](#table-of-contents)
Events in react are done thought attributes.

```javascript
function Component(){
  function handleClick(name){
    alert(name)
  }

  return (
    <>
      <button onClick={handleClick}>Click Me</button>
      <button onClick={() => {console.log("clicked")}}>Click Me</button>
      <button onClick={handleClick("Ryan")}>Click Me</button> {/*This will invoke the function immediately. It will display the alert right away.*/}
      <button onClick={() => handleClick("Ryan")}>Click Me</button> {/* Instead do this to make the alert popup when the button is clicked. This is used for passing arguments into function in JSX*/}
    </>
  )
}
```

| Common events | Description |
|---------------|-------------|
| onClick       |             |
| onMouseOver   |             |
| onMouseOut    |             |
| onSubmit      |             |
| onChange      |             |
| onKeyDown     |             |
| onKeyUp       |             |
| onFocus       |             |
| onBlur        |             |
| onDoubleClick |             |
| onContextMenu |             |
| onTouchStart  |             |

## [Tailwind in React](#table-of-contents)

1. `npm install tailwindcss postcss autoprefixer --save-dev`
2. Generate Tailwind Css config files `npx tailwindcss init -p`
3. Add this to content array in tailwind.config.js

```
  content: [
    "./index.html",
    "./src/**/*.{js,ts,jsx,tsx}",
  ],
```

4. Add these lines to the top of index.css

```
@tailwind base;
@tailwind components;
@tailwind utilities;
```

### [Changing Tailwind with State](#table-of-contents)

Tailwind will only include classes with the full name of that class meaning you cannot use string concatenation inside a className.

```javascript
const [error, setError] = useState(false)

// This will not work
<div className="text-{{ error ? 'red' : 'green' }}-600"></div>

// This will work
<div className="{{ error ? 'text-red-600' : 'text-green-600' }}"></div>
```

In order to have dynamic variables you have to use style.

```javascript
const width = "200px"

// This will not work
<div className="></div>

// This will work
```

## [useState](#table-of-contents)
  - State
    - Just an object. Something that changes on the website that changes between 2 unique visitors to a page.
      - Count button. 2 users have different experiences depending on how many times they click it
        - this.setState
      - Changes on between 2 or more different visitors
State is used for variables that when changed should cause a re-render on the screen. These tend to be variables that are different for each client who visits the site.

useState tells React that something has changed to the DOM so react can re-render the DOM.

In react when a page is re-rendered(because of a state change) then the component function is ran again to return the JSX.

```javascript
import { useState } from 'react';

export default function Counter() {
  // Array destructing
  const [count, setCount] = useState(0/*Initial value of state*/);
    // count is the value of the state at that moment. Get variable
    // setCount is used to update the state. Set method

  const handleClick = () => {
    setCount((count + 1)) // Takes time to update the count. Can't use async/await
    count += 1 // This will change the state, but it won't tell react to update the DOM so you don't see the changes
    console.log(`New value of count: ${count}`); // Previous value of count because setCount hasn't had time to update count
  };

  return (
    <div className="card text-center">
      <div className="card-header bg-primary text-white">Click Counter!</div>
      <div className="card-body">
        <p className="card-text">Click Count: {count}</p>
        <button className="btn btn-primary" type="button" onClick={handleClick}>
          Increment
        </button>
      </div>
    </div>
  );
}
```

## [Forms in React](#table-of-contents)
States are used to update the values in forms as to allow for setState to update the form.

If you didn't have `value={state}` then the values in the form won't be set with `setState("")` and instead be left to their original inputs.

```javascript
import { useState } from 'react';
import './style.css';

function Form() {
  const [firstName, setFirstName] = useState('');
  const [lastName, setLastName] = useState('');

  const handleInputChange = (event) => {
    const { name, value } = event.target;

    return name === 'firstName' ? setFirstName(value) : setLastName(value);
  };

  const handleFormSubmit = (event) => {
    event.preventDefault();

    alert(`Hello ${firstName} ${lastName}`);
    setFirstName('');
    setLastName('');
  };

  return (
    <div className="container text-center">
      <h1>
        Hello {firstName} {lastName}
      </h1>
      <form className="form" onSubmit={handleFormSubmit}>
        <input
          value={firstName/*State variable*/}
          name="firstName"
          onChange={handleInputChange}
          type="text"
          placeholder="First Name"
        />
        <input
          value={lastName}
          name="lastName"
          onChange={handleInputChange}
          type="text"
          placeholder="Last Name"
        />
        <button type="submit">
          Submit
        </button>
      </form>
    </div>
  );
}

export default Form;
```

## [useEffect](#table-of-contents)
useEffect is used to run code based upon some variable changing.

useEffect is often used for things in the app that need to interact with the external world like API requests, localstorage, etc. These are called sideEffects.

You can think of these as event driven code.

useEffect never returns anything

```javascript
import {useEffect, useState, useRef} from "react"

const [state1, setState1] = useState(true)
const [state2, setState2] = useState(true)

const stateRef = useRef({state1, state2})

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

useEffect(() => {
  if(stateRef.current.state1 !== state1 && stateRef.current.state2 !== state2){
    // Only when both the state1 and state2 changes this code is ran
    stateRef.current = {state1, state2}
  }
}, [state1, state2])
```

Why does useEffect [] run twice on reload when useStrick is being used on your react app.

## [useRef](#table-of-contents)
Used to set variables without causing a re-render of the DOM.

## [Testing in React](#table-of-contents)
vitest
npx vitest
happy-dom
@teesting-library

in vite.config.js
```javascript
test: {
  globals: true, // VI keywords globally. DOn't need to import
  environment: "happy-dom",
  setupFiles: "./src/tests/setup.js"
}
```

src/tests
  setup.js
  welcome.text.jsx

```javascript

```

`npm install react-dom --save-dev`
react-dom gives DOM-specific methods for working with React. It is used to render React components into the DOM.

```javascript
import ReactDOM from "react-dom"

// Render a React component into a DOM element
ReactDOM.render(<App />, document.querySelector("#root")) // Puts app component in component with id "root"

// Remove component from DOM and cleans up its event handlers and state
  // What does this do and why is it needed?
ReactDOM.unmountComponentAtNode(container)
```