# Setup A React App From Scratch

Use Babel and webpack to take in React components and output JavaScript for the browser.

## Setup a project folder

Create a new project folder and *package.json* file:

```bash
mkdir -p setup-react-from-scratch/src
cd setup-react-from-scratch
npm init -y
```

## Setup Babel

1. Babel with **@babel/core**
2. Transpile JavaScript ES6 to JavaScript ES5 with **@babel/preset-env** 
3. Transpile React/JSX to JavaScript with **@babel/preset-react**

Install Babel and presets:

```bash
npm install @babel/core --save-dev
npm install @babel/preset-env --save-dev
npm install @babel/preset-react --save-dev
```

Create a new *.babelrc* file:

```js
{
  "presets": ["@babel/preset-env", "@babel/preset-react"]
}
```

## Setup webpack

1. Bundle JavaScript with **webpack**
2. Interface with webpack through a cli with **webpack-cli**

Install webpack:

```bash
npm install webpack --save-dev
npm install webpack-cli --save-dev
```

Without additional components webpack only processes JavaScript.
Loaders can be used to transform (transpile) other resources into JavaScript for webpack.
Additonally, an HTML plugin can be used to generate HTML files.

1. Babel webpack loader with **babel-loader**
2. Inject CSS into the DOM with **style-loader**
3. CSS webpack loader with **css-loader**
4. HTML webpack loader with **html-loader**
5. Generate HTML files with **html-webpack-plugin**

Install webpack loaders and plugin:

```bash
npm install babel-loader --save-dev
npm install style-loader --save-dev
npm install css-loader --save-dev
npm install html-loader --save-dev
npm install html-webpack-plugin --save-dev
```

A webpack development server can be used to launch the application in a
browser on start and refresh the browser after modifications.

1. Development server for webpack with **webpack-dev-server**

Install webpack development server:

```bash
npm install webpack-dev-server --save-dev
```

Edit the *"script"* command in the *package.json* file:

```js
"scripts": {
  "start": "webpack-dev-server --open --mode development",
  "build": "webpack --mode production"
}
```

Configure webpack to run *.js*, *.jsx*, *.css*, and *.html* files through the loaders,
and then generate a new *index.html* file from a template in *src/index.html*.

Create a new *webpack.config.js* file:

```js
const HtmlWebPackPlugin = require("html-webpack-plugin");

module.exports = {
  module: {
    rules: [
      {
        test: /\.(js|jsx)$/,
        exclude: /node_modules/,
        use: {
          loader: "babel-loader"
        }
      },
      {
        test: /\.css$/,
        use: [
          "style-loader", 
          "css-loader"
        ]
      },
      {
        test: /\.html$/,
        use: {
            loader: "html-loader"
        }
      }
    ]
  },
  plugins: [
    new HtmlWebPackPlugin({
      template: "./src/index.html",
      filename: "./index.html"
    })
  ]
};
```

Create a new *src/index.html* template file:

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>Setup React App</title>
  </head>
  <body>
    <noscript>You need to enable JavaScript to run this app.</noscript>
    <div id="root"></div>
  </body>
</html>
```

Create a new *src/index.css* file:

```css
body {
  background-color: #282c34;
  font-family: sans-serif;
}

code {
  font-family: monospace;
}

.App {
  max-width: 500px;
  margin: 50px auto;
  border: 2px solid #61dafb;
  background-color: #282c34;
  color: #61dafb;
  text-align: center;
  
}
```

## Setup React

1. React with **react**
2. Access and modify the DOM with **react-dom**

Install React:

```bash
npm install react --save-dev
npm install react-dom --save-dev
```

Create a new *src/App.js* file:

```js
import React from 'react';

function App() {
  return (
    <div className="App">
        <h2>
          Edit <code>src/App.js</code> and save to reload
        </h2>
    </div>
  );
}
export default App;
```

Create a new *src/index.js* file:

```js
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './App';

ReactDOM.render(<App />, document.getElementById('root'));
```

## Bundle with webpack

Create a webpack bundle:

```bash
npm run build
```

This will create a new *dist/index.html* file and a new *dist/main.js* file.

Alternatively, use the webpack development server to launch the application in a browser:

```bash
npm start
```
