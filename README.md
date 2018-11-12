## workshop-for-novice-front
fast start developing frontend applications with Webpack and React

#### step 1 - prepare environment:

* install Nodejs from https://nodejs.org (to enable node package manager (npm) support)
* init new package through command line: `npm init` (enter for default answers)
* install React and Webpack with plugins and loaders: 

```$xslt
npm i -D react react-dom webpack webpack-cli webpack-dev-server copy-webpack-plugin clean-webpack-plugin html-webpack-plugin source-map-loader babel-loader @babel/core @babel/preset-env @babel/preset-react style-loader css-loader
npm i -g webpack-cli
``` 

* edit generated package.json file: add start and build scripts into "scripts" section (generated "test" script can be 
removed): 
```$json
"scripts": {
    "start": "webpack-dev-server",
    "build": "webpack"
}, 
```

FYI:

Webpack is a multipurpose builder for frontend applications. It lets you write modular code and bundle it together. 
Additional functionality can be enabled via:
 * plugins https://webpack.js.org/plugins/ - copy files, clear directories, generate html from template, etc.
 * loaders https://webpack.js.org/loaders/ - preprocess files, transpiling them from one format to another. For 
 instance: ts -> js, pug/jade -> html, sass/scss/postCSS/less -> css, etc. and load them as modules. 
 
React is a library which gives ability to create Views using JSX syntax and components, making UI development much 
painless than ever before, because it enforce composition over inheritance model (js is a functional language and 
composition model is functional approach, while inheritance came from OOP and fits really bad for js development). 
From docs: "React has a powerful composition model, and we recommend using composition instead of inheritance to 
reuse code between components."

Babel lets you transpile modern JavaScript/JSX code and enable support for older browsers.

#### step 2 - webpack configuration:

* create file `webpack.config.js` in project directory. It will contain webpack settings:

```$js
const path = require("path");
const webpack = require("webpack");
const CleanWebpackPlugin = require("clean-webpack-plugin");

module.exports = {
  // entry point for webpack builder to start process with application
  entry: "./src/index.jsx",
  // development | production mode presets
  mode: "development",
  // source mappings
  devtool: 'source-map',
  // set of rules for files preprocessing with loaders
  module: {
    rules: [
      {
        test: /\.(js|jsx)$/,
        exclude: /node_modules/,
        loader: "babel-loader",
        options: { presets: ["@babel/env", "@babel/react"] }
      },
      {
        test: /\.css$/,
        use: ["style-loader", "css-loader"]
      }
    ]
  },
  // which file extensions will be treated as modules (can be imported)
  resolve: { extensions: ["*", ".js", ".jsx"] },
  // where to write generated files (bundle.js, etc)
  output: {
    path: path.resolve(__dirname, "dist/"),
    publicPath: "/dist/",
    filename: "bundle.js"
  },
  // dev-server settings
  devServer: {
    port: 8080,
    hotOnly: true
  }, // plugins section
  plugins: [
    // clean directory before build
    new CleanWebpackPlugin(['dist']),
    // replacing modules in real time after updates
    new webpack.HotModuleReplacementPlugin()
  ]
};
```

#### step 3 - application core:

now let's add some core application files:
* index.html in project root folder, containing "div" with id = "root" and generated script "bundle.js" from dist 
folder:
```$html
<!doctype html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
</head>
<body>
    <div id="root"></div>
    <script src="dist/bundle.js"></script>
</body>
</html>
```

* src/index.jsx - app entry point file that will render our App component into div with "root" id:
```$jsx
import * as React from 'react';
import {render} from 'react-dom';
import {App} from './App'

render(<App/>, document.getElementById('root'));
``` 

* App.jsx - file with App component:
```$jsx
import * as React from 'react';
import './App.css';

export class App extends React.Component {
  render () {
    return <div>Hello world</div>
  }
}
```

* App.css - for styles:
```$css
body {
    margin: 0;
}
```

FYI:
* importing css available due to style-loader and css-loader in webpack configuration.
* 

#### We can now launch application by executing `npm run start` in console, it will be available at http://localhost:8080/