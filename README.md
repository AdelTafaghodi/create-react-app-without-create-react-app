# create react app without create-react-app

1.
```
npm init
```
 
2.
 ```
 npm install react react-dom
 ```
 
3.
 ```
 npm install --save-dev webpack webpack-cli webpack-dev-server
 ```
 
4.
 ``` 
 npm install --save-dev @babel/core @babel/preset-env @babel/preset-react babel-loader
 ```
 
5. Create a file .babelrc and copy the code below : 
```js
{
 "presets": [
        "@babel/preset-react",
        "@babel/preset-env"
            ]
}
 ```
 
6.
```
npm install --save-dev html-webpack-plugin style-loader css-loader file-loader
```

7. Create a file webpack.config.js and copy the code below:
```js
const HtmlWebpackPlugin = require("html-webpack-plugin");
const path = require("path");

module.exports = {
  entry: "./src/index.js",
  output: {
    filename: "bundle.[hash].js",
    path: path.resolve(__dirname, "dist"),
  },
  plugins: [
    new HtmlWebpackPlugin({
      template: "./src/index.html",
    }),
  ],
  resolve: {
    modules: [__dirname, "src", "node_modules"],
    extensions: ["*", ".js", ".jsx", ".tsx", ".ts"],
  },
  module: {
    rules: [
      {
        test: /\.jsx?$/,
        exclude: /node_modules/,
        loader: require.resolve("babel-loader"),
      },
      {
        test: /\.css$/,
        use: ["style-loader", "css-loader"],
      },
      {
        test: /\.png|svg|jpg|gif$/,
        use: ["file-loader"],
      },
    ],
  },
};
```

8. Create a folder “src” and inside that create a file “App.js” :
```js
import React from "react";

const App = () => (
    <div>
        <h1>Hello React</h1>
    </div>
);

export default App;
```

9.Create a file “index.js” that will be the entry point of our code:
```js
import React from "react";
import ReactDOM from "react-dom";
import App from "./App";

ReactDOM.render(<App/>,document.querySelector("#root"));
```

10.Create another file “index.html” :
```html
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>React</title>
</head>

<body>
    <div id="root"></div>
</body>

</html>
```

11.In your package.json write the following lines of code in place of the script tag:
```js
"scripts": {
    "start": "webpack serve  --hot --open",
    "build": "webpack --config webpack.config.js --mode production"
}
```

12.:tada:
```
npm start
```
