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
  - [Conditional Rendering](#conditional-rendering)
  - [Map function in React](#map-function-in-react)
  - [Event handling in React](#event-handling-in-react)
  - [Tailwind in React](#tailwind-in-react)
  - [useState](#usestate)
  - [Forms in React](#forms-in-react)
  - [useEffect](#useeffect)
  - [useRef](#useref)

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
  - Short circuit operators

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

You can rin JavaScript inside JSX with {}s. Whatever the js in the {}s returns is converted into a string, including arrays, so it can be embedded in the JSX.

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

Component

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

## [Conditional Rendering](#table-of-contents)

```javascript
 {props.message &&
  <div>Some JSX</div>
 }

 // It is recommended to do
 {props.message ?
  <div>Some JSX</div> :
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
3. Add these lines to index.css
```
@import 'tailwindcss/base';
@import 'tailwindcss/components';
@import 'tailwindcss/utilities';
```
4. Build the tailwind.css file by adding this to your package.json and then run `npm run build:tailwind`
```
"scripts": {
  "build:tailwind": "tailwindcss build src/index.css -o public/tailwind.css"
}
```
5. Include link in your index.html file
```
<link href="public/tailwind.css" rel="stylesheet">
```

## [useState](#table-of-contents)
  - State
    - Just an object. Something that changes on the website that changes between 2 unique visitors to a page.
      - Count button. 2 users have different experiences depending on how many times they click it
        - this.setState
      - Changes on between 2 or more different visitors

useState tells React that something has changed to the DOM so react can re-render the DOM.

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
  // When the state changes this code is ran
}, [state1])

useEffect(() => {
  // When the state1 or state2 changes this code is ran
}, [state1, state2])

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