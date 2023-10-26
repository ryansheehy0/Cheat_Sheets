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

Explain and use the npm create vite@latest command line utility to create new React projects.
Explain and use JSX to render elements on the page.
Isolate code into reusable components and explain the benefits of doing so.
Explain and use Props to pass data to child React components.

## Questions:
  - Single page app vs multi-page app
  - Props
  - State
    - Just an object. Something that changes on the website that changes between 2 unique visitors to a page.
      - Count button. 2 users have different experiences depending on how many times they click it
        - this.setState
      - Changes on between 2 or more different visitors
  - Hooks
    - State and other react features without writing classes. Can put them in functions.
    - Don't need this.setState
  - Short circuit operators

## Virtual DOM
The Virtual DOM is an object in memory that represents the real DOM.

The virtual DOM is synced with the DOM which is called reconciliation.

When you change the DOM in React the virtual DOM is changed. Its compared with the old virtual DOM. It tries to batch any changes and then it changes the DOM all at once.

## JSX
If it starts with a capital letter then it knows its JSX and not html


### Fragments
Fragments are empty tags <></> that go around all the JSX components.

Functions can only return 1 value. The fragments allow you to return multiple component values as 1 single value to allow it to be returned.


className vs class
class is a protective work for css
className is 

Javascript goes in {}s in JSX
Comments
{/* Comments */}
Array of strings in {}s gets put as one string.

Every tag needs to tbe closed or self closed. </> or />. Can't have things like `<hr>`

## Vite
Vite build tool for react.
- Fast Development Server
- On Demand compilation
- Hot reloading
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

## File Structure

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



## Components
Each component tends to go in its own file.

```javascript
// Arguments into components?
function HelloReact(){
  const text = "some text"

  return <h2>Hello Workd! Here is {text}</h2>
  // If you want to return with multiple lines
  return (
    <h2>
      Hello Word! Here is {text}.
    </h2>
  )

}

export default HelloReact
```

### CSS in Components

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

### Props
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

| Reserved attribute             | Description |
|--------------------------------|-------------|
| key                            |             |
| ref                            |             |
| children                       |             |
| dangerouslySetInnerHTML        |             |
| defaultValue | |
| defaultChecked | |
| suppressContentEditableWarning |             |
| suppressHydrationWarning       |             |
| className                      |             |
| class                      |             |
| style                          |             |

## Conditional Rendering

```javascript
 {props.message &&
  <div>Some JSX</div>
 }
```