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
