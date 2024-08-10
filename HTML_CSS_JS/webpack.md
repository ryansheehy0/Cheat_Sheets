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

[Home](../README.md)

# Webpack
Webpack is a bundler that takes your javascript, css, images, etc and bundles them into 1 file or multiple files that.

Why use webpack
- Allows for `import` and `export` keywords in you client side javascript.
- Don't have to load all your client side javascript files in your html in the correct order.
- Allow for hot reloading. Don't have to manually reload browser to see changes.

<!-- TOC -->

- [webpack.config.js](#webpackconfigjs)
- [Separate HTML file](#separate-html-file)
- [Separate CSS file](#separate-css-file)
- [Favicon](#favicon)
- [Hot Reloading](#hot-reloading)
- [Include Service Worker](#include-service-worker)
	- [GenerateSW](#generatesw)
		- [Runtime Caching](#runtime-caching)
	- [Inject Manifest](#inject-manifest)
- [Babel](#babel)
- [PWA Manifest](#pwa-manifest)

<!-- /TOC -->

## [webpack.config.js](#webpack)
`npm install webpack webpack-cli --save-dev`

```javascript
// Includes
const path = require('path')

module.exports = {
  mode: 'development',
  entry: './src/js/index.js', // Look first to build out the bundle
  output: {
    filename: 'bundle.js', // Output js file name
    path: path.resolve(__dirname, 'dist'), // Path where to to output. Using file called dist which stands for distribution
  },
  plugins: [
    /*
    Plugins
    */
  ],
  module: {
    rules: [
      /*
      How webpack should process different files
      */
      {
        test: /\.(png|svg|jpg|jpeg|gif)$/i,
        type: 'asset/resource',
      },
    ],
  },
}
```

You don't need to include your css or js in your html.

Run `npm run build` or `npx webpack` in order to build the webpack.

## [Separate HTML file](#webpack)
`npm install html-webpack-plugin --save-dev`

```javascript
// imports
const HtmlWebpackPlugin = require('html-webpack-plugin')

// Plugins
plugins: [
  new HtmlWebpackPlugin({
    template: './index.html', // Optional. Name of outputted html file
  }),
]
```

## [Separate CSS file](#webpack)
`npm install style-loader css-loader mini-css-extract-plugin --save-dev`

The reason to extract the css in a different file is to load the JS and the CSS at the same time.

```javascript
// imports
const MiniCssExtractPlugin = require('mini-css-extract-plugin')

// Plugins
plugins: [
  new MiniCssExtractPlugin(),
]

// Rules
rules: [
  {
    test: /\.css$/i, // Looks for .css files
    use: [MiniCssExtractPlugin.loader, 'css-loader'],
  },
]
```

## [Favicon](#webpack)
`npm install favicons-webpack-plugin --save-dev`

```javascript
// imports
const FaviconsWebpackPlugin = require('favicons-webpack-plugin')

// Plugins
plugins: [
  new FaviconsWebpackPlugin({
    logo: "./favicon.ico"
  })
]
```

## [Hot Reloading](#webpack)
`npm install webpack-dev-server --save-dev`

```javascript
// Inside module.exports
module.exports = {
  devServer: {
    hot: 'only'
  },
}
```

To allow for Hot Module Reloading(HMR), reloading on save including the webpage, add `"dev": "webpack-dev-server --open"` in your package.json under scripts. Then run `npm run dev`

In your index.js file add this code to the bottom

```javascript
if(module.hot){
  module.hot.accept((err) => {
    if(err){
      console.error("Cannot apply HMR update.", err)
    }
  })
}
```

## [Include Service Worker](#webpack)
`npm install workbox-webpack-plugin --save-dev`

```javascript
// imports
const WorkboxPlugin = require("workbox-webpack-plugin")
```

### [GenerateSW](#webpack)

```javascript
// plugins
plugins: [
  new WorkboxPlugin.GenerateSW(),
]
```

#### [Runtime Caching](#webpack)
Runtime caching is used to prevent too much pre-caching which will download a lot of content that the user may never see. This pre-caching may cause things to slow down when the site first loads.

These are often used with images because they take up a lot of space.

```javascript
// plugins
plugins: [
  new WorkboxPlugin.GenerateSW({
    exclude: /\.(png|jpg|jpeg|gif)$/, // Don't cache files ending in those extensions
    runtimeCaching: [{
      urlPattern: /\.(png|jpg|jpeg|gif)$/,
      handler: "CacheFirst", // Service worker will look for resource in cache first
      options: {
        cacheName: "images-cache",
      }
    }]
  }),
]
```

### [Inject Manifest](#webpack)
Inject manifest function is used to give more customization to your service worker.

```javascript
// Plugins
plugins: [
  new WorkboxPlugin.InjectManifest({
    swSrc: './src-sw.js', // Your custom service worker code
    swDest: 'service-worker.js',
  }),
]
```

./src-sw.js file:

```javascript
```

## [Babel](#webpack)
Babel is used to convert ES6 to ES5 to allow for your app to work in older browsers.

Babel allows modern js to be able to run on old browsers.

`npm install babel-loader @babel/core @babel/preset-env --save-dev`

```javascript
// Rules
rule: [
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
]
```

## [PWA Manifest](#webpack)
`npm install webpack-pwa-manifest --save-dev`

```javascript
// imports
const WebpackPwaManifest = require('webpack-pwa-manifest')

// plugins
plugins: [
  new WebpackPwaManifest({
    name: "",
    short_name: "",
    description: "",
    start_url: "/",
    theme_color: "#225ca3",
    background_color: "#225ca3",
    orientation: "portrait",
    display: "standalone",
    icons: [
      {
        src: path.resolve("src/images/logo.png"),
        sizes: [96, 128, 192, 256, 384, 512],
        destination: path.join("assets", "icons") // Output is /assets/icons/
      }
    ],
    fingerprints: false, // Removes the fingerprint ont he manifest and icons
    publicPath: "/" // Path to manifest.json in linked html
  }),
]
```