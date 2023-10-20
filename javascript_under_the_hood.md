[Home](./README.md)

# JavaScript Under the Hood
Javascript is single threaded language. The thread has a call stack and memory heap. This cheat sheet goes through how those things work and other things on how javascript works under the hood.

## Table of Contents

<!-- TOC -->

- [JavaScript Under the Hood](#javascript-under-the-hood)
  - [Table of Contents](#table-of-contents)
  - [LIFO/FIFO](#lifofifo)
  - [Call Stack](#call-stack)
    - [Example 1](#example-1)
    - [Example 2](#example-2)
  - [Callback Queue and Event Loop](#callback-queue-and-event-loop)
  - [Global and Function Execution Context](#global-and-function-execution-context)
  - [Use Strick](#use-strick)
  - [Useful terms](#useful-terms)
  - [Closures](#closures)
    - [Var/Let strick question](#varlet-strick-question)
  - [Big O Notation](#big-o-notation)
  - [Progressive Web AppsPWA](#progressive-web-appspwa)
    - [Manifest](#manifest)
    - [Service worker](#service-worker)
      - [Push notifications](#push-notifications)
  - [Webpack](#webpack)
    - [Babel](#babel)
    - [Inject Manifest](#inject-manifest)
  - [Lighthouse](#lighthouse)
  - [Client-Server Folder Layout](#client-server-folder-layout)

<!-- /TOC -->

## [LIFO/FIFO](#table-of-contents)
**LIFO** - Last in first out.
- The last thing added is going to be the first thing out.
- Like a stack of plates where you take one from the top.

**FIFO** - First in first out.
- The first thing added is going to be the first thing out.
- Like a queue of people. The person who was first in line gets pulled out first.

## [Call Stack](#table-of-contents)
The call stack is LIFO and is a list of functions that need to be ran. The bottom is always the Global Execution Context.

### [Example 1](#table-of-contents)

```javascript
function first(){console.log("first")}
function second(){console.log("second")}
function third(){console.log("third")}

first()
second()
third()
```

         | Call Stack |
---------|------------|---------
third -> | second     | -> first
         | Global EV  |

### [Example 2](#table-of-contents)
When you have functions inside functions it is added to the call stack.

```javascript
function first(){
  console.log("first")
  second()
}

function second(){
  console.log("second")
  third()
}

function third(){
  console.log("third")
}

first()
```

| Call Stack |
|------------|
| third      |
| second     |
| first      |
| Global EC  |

## [Callback Queue and Event Loop](#table-of-contents)
[This](https://www.youtube.com/watch?v=8aGhZQkoFbQ&list=WL&index=3) is a good resource.

When an `async` function is called it runs synchronously like any other function. If an `await` is encountered, it passes the code to the webAPI or the NodeAPI.

The webAPIs or the NodeAPIs run in a different threads and are called when async operations need to be performed.

When the async operation finishes, like the timer in `setTimeout` or `fetch` gets back data, the callback function(with async, the code after the await) is added to the callback queue.

The event loop checks if the callback stack is empty. If it is empty it checks for the next callback function in the event queue. It then puts that function in the callback stack.

The synchronous functions always have higher priority than any function in the callback queue.

## [Global and Function Execution Context](#table-of-contents)
The global execution context is the outermost scope in JS.

The function execution context is created when a function is invoked and variables declared in the function can only be used in the function.

## [Use Strick](#table-of-contents)
Use strick is used to convert bad syntax to errors.

To use use strick you can either put `"use strick"` at the top of your js file or put `"use strick"` at the top of functions to just use strick for that function.

- Can't use un-declared variables.
  - You have ot first create a variable with var, const, or let
- You can't delete a variable
  - Ex: `const x = 5; delete x;` will throw an error
- No duplicate argument names in functions
- `this` is undefined for functions that aren't methods
- Can't use `with` or `eval` keyword

## [Useful terms](#table-of-contents)

| Term                   | Definition                                  |
|------------------------|---------------------------------------------|
| Higher order functions | Functions with other functions as arguments |
| Shallow copy           | Pass by reference                           |
| Deep copy              | Pass by value                               |
| Lexical Envurornemrn   |                                             |

## [Closures](#table-of-contents)
Closures are functions that are returned from another function, that allow you to access private variables in the outer function.

When a function is returned a closure, in the backend, is made which holds the private variables.

```javascript
function bankAccount() {
  const checking = 400
  const savings = 1000

  return {
    displayFunds: function () {
      console.log(`You have $${checking} in your checking account and $${savings} in your savings account`)
    },
  }
}
```

Factory functions are like closures, but are given arguments.

### [Var/Let strick question](#table-of-contents)

```javascript
// var is scoped to the global scope therefore it doesn't change closures
// If i were let it would be scoped to the for loop and would have its own closure.
  // If it was let it would be 0, 1, 2
for(var i = 0; i < 3; i++){
  const log = () => {
    consol.log(i)
  }

  setTimeout(log, 100)
}

// This will output 3 3 3
```

## [Big O Notation](#table-of-contents)
Because an increasingly complex computer can run any algorithm faster, in order to compare algorithms we use a standard notation called Big O Notation.

Big O Notation removes any constants and only accounts for the number of inputs so you don't have to worry about different computers.

Big O notation uses the syntax of O().

This is the efficiency in order of worst to best when n is very large.
  - O(n!), O(2^n), O(n^2), O(n log n), O(n), O(log n), O(1)

The Big O of a for loop is O(n)

The Big O of a nested for loop in another for loop is O(n^2)

Big O notation is always the worst case scenario

## [Progressive Web Apps(PWA)](#table-of-contents)
A progressive web app(PWA) is a web application that performs like a native app.
- Installable on the device
  - Run in a headless browser
- Can work offline
- Can have a splash screen
- Needs to run over HTTPS
- Assets are downloaded and bundled which often leads to faster performance.
- Has access to device specific API features
  - Push notifications
  - Bluetooth
  - File system Access
  - Geolocation
  - Clipboard
  - There maybe device features not allowed for PWAs

Need to research
- service worker
  - Thread that works in the background. Caching, background sync, push notifications.
- client side database
- userAgent
- indexedDB

When you code for a PWAs you need to check if a feature is there in order to use it.

This is js on the front end.

```javascript
// Note: window.navigator. is the same as navigator.
if("serviceWorker" in navigator){}
if("bluetooth" in navigator){}
if("geolocation" in navigator){
  navigator.geolocation.getCurrentPosition()
}
if("contacts" in navigator && "ContactsManager" in window){
  const props = ["name", "email", "tel", "address", "icon"]
  const opts = {multiple: true} // Allows selecting multiple contacts
  const contacts = await navigator.contacts.select(props, opts)
}
// etc
```

### [Manifest](#table-of-contents)
Meta data and settings for the PWA.

https://developer.mozilla.org/en-US/docs/Web/Manifest/

The only settings that are required are name and short_name

```javascript
{
  "name": "Web App Name",
  "short_name": "name", // Name on the device home screen or app launcher
  "description": "The description of the web app.",
  "start_url": "/", // Specifies the starting url path when the PWA is launched. Ex: "start_url": "/home" will be https://yourwebsite.com/home
  "icons": [
    {
      "src": "icons/icon-32.png",
      "sizes": "32x32",
      "type": "image/png"
    },
    // More icons
  ],
  "display": "standalone", // fullscreen(Puts the webapp in fullscreen like a video), standalone(standalone app), minimal-ui(mini ui for controlling navigation), browser(normal browser tab)
  "theme_color": "#4285F4", // The ui color theme of the browser
  "background_color": "#FFFFFF", // Sets the background color of the splash screen
}
```

You have to link the manifest file in your html

`<link rel="manifest" href="/manifest.json">`

### [Service worker](#table-of-contents)
The service worker is a separate thread that runs in the background which allows for offline functionality, push notification, and background synchronization(app updates even if its not on the screen).
install activate claim

In your main js file

```javascript
// Register the service worker
if ('serviceWorker' in navigator) {
  navigator.serviceWorker.register('/service-worker.js')
    .then(registration => {
      console.log(`Service Worker registered: ${registration}`)
    })
    .catch(error => {
      console.error(`Error registering Service Worker: ${error}`)
    })
}
```

In your service-worker.js file in the client

This can all be automatically generated by `workbox-webpack-plugin`

```javascript
const cacheName = "my-cache-name"

// Install the service worker. Cache the files
self.addEventListener('install', event => {
  event.waitUntil(
    caches.open(cacheName).then(cache => {
      return cache.addAll([ // The files built by webpack
        '/',
        '/index.html',
        '/bundle.js',
        '/images/logo.png'
      ])
    })
  )
})

// Activate the service worker. Used to clean up past caches
self.addEventListener("activate", (event) =>
  event.waitUntil(
    caches.keys().then((keyList) =>
      Promise.all(
        keyList.map((key) => {
          if (key !== cacheName) {
            return caches.delete(key)
          }
        })
      )
    )
  )
)

// Claim the service worker so the service worker intercepts requests to other servers
  // Server/Websites -> Service worker -> Client's webpage
self.addEventListener("activate", (event) => {
  event.waitUntil(clients.claim())
})

// When a request is fetched
self.addEventListener("fetch", event => {
  event.respondWith((async () => {
    // Check if resource is cached and if so return cache
    const result = await caches.match(event.request)
    if(result) return result
    // If not, retrieve the resource
    const response = await fetch(event.request)
      // Cache it, and then return it. You may not want this
        // const cache = await caches.open(cacheName)
        // cache.put(event.request, response.clone())
    return response
  })())
})
```

#### [Push notifications](#table-of-contents)


## [Webpack](#table-of-contents)
Webpack is a bundler that takes your javascript, css, images, etc and bundles them into 1 file or multiple files.

Webpack supports
- importing and exporting
  - Don't have to put scripts in your html in a specific order. Just have to link the bundled js file in your html
- Removes unused code
  - Like duplications in node modules

NPM installs
- `npm install webpack webpack-cli style-loader css-loader html-webpack-plugin webpack-dev-server mini-css-extract-plugin workbox-webpack-plugin --save-dev`

webpack.config.js

```javascript
const HtmlWebpackPlugin = require('html-webpack-plugin')
const MiniCssExtractPlugin = require('mini-css-extract-plugin')
const WorkboxPlugin = require("workbox-webpack-plugin")
const path = require('path')

module.exports = {
  mode: 'development',
  entry: './src/js/index.js', // Look first to build out the bundle
  devServer: {
    hot: 'only' // use the hot module reloading api
  },
  output: {
    filename: 'bundle.js', // Output js file name
    path: path.resolve(__dirname, 'dist'), // Path where to to output. Using file called dist which stands for distribution
  },
  plugins: [
    new HtmlWebpackPlugin({
      template: './index.html', // Optional. Name of outputted html file
    }),
    new MiniCssExtractPlugin(),
    new WorkboxPlugin.GenerateSW({
      // Runtime caching is used to
        // prevent too much pre-caching which will download a lot of content that the user may never see. This pre-caching may cause things to slow down when they are downloading.
      exclude: /\.(png|jpg|jpeg|gif)$/, // Don't cache files ending in those extensions
      runtimeCaching: [{
        urlPattern: /\.(png|jpg|jpeg|gif)$/,
        handler: "CacheFirst", // Service worker will look for resource in cache first
        options: {
          cacheName: "images-cache",
        }
      }]
    }),
  ],
  module: {
    rules: [
      {
        test: /\.css$/i, // Looks for .css files
        use: [MiniCssExtractPlugin.loader, 'css-loader'],
      },
      {
        test: /\.(png|svg|jpg|jpeg|gif)$/i,
        type: 'asset/resource',
      },
    ],
  },
}
```

You don't need to include your css or js in your html.

Run `npm run build` or `npx webpack` in order to build the webpack with your webpack,.

To allow for hot module reloading(HMR), reloading on save including the webpage, add `"dev": "webpack-dev-server --open"` in your package.json under scripts. Then run `npm run dev`

In your main js file add this code at the bottom

```javascript
if(module.hot){
  module.hot.accept((err) => {
    if(err){
      console.error("Cannot apply HMR update.", err)
    }
  })
}
```

### [Babel](#table-of-contents)
Convert ES6 to ES5

Allows modern js to be able to run on old browsers.

`npm install babel-loader @babel/core @babel/preset-env --save-dev`

Add to rules in the webpack.config.js

```javascript
    {
      test: /\.m?js$/,
      exclude: /(node_modules|bower_components)/,
      use: {
        loader: 'babel-loader',
        options: {
          presets: ['@babel/preset-env']
        }
      }
    },
```

### [Inject Manifest](#table-of-contents)
Used to customize the autogenerated service-worker.js more than with GenerateSW.

It uses the same `workbox-webpack-plugin` npm package

Inside webpack.config.js

```javascript

// Inside plugins. Instead of new WorkboxPlugin.GenerateSW
  new WorkboxPlugin.InjectManifest({
    swSrc: './src/sw.js',
    swDest: 'service-worker.js',
  }),
```

## [Lighthouse](#table-of-contents)
Test the performance, accessability, SEO, and other things for your web app.

Inspect element and Lighthouse tab.

## [Client-Server Folder Layout](#table-of-contents)
You want to separate the package.json/dependencies into separate client and server side for organization reasons.

```
client
  - uses webpack
  - dist
  - src
  - package.json
server
  - uses express
  - package.json
package.json
```

In your express server add `app.use(express.static("../client/dist"))` in order to load the webpack built files which are usually in the dist folder inside client.

In the main package.json file

Scripts

```javascript
{
  "name": "13-ins_client-server",
  "version": "1.0.0",
  "main": "index.js",
  "license": "MIT",
  "scripts": {
    "start": "concurrently \"cd client && npm run build\" \"cd server && npm run server\" ",
    "server": "cd server && npm run server",
    "build": "cd client && npm run build",
    "install": "cd server && npm i && cd ../client && npm i",
    "client": "cd client && npm start"
  },
  "devDependencies": {
    "concurrently": "^5.2.0"
  }
}
```

Run `npm run start`