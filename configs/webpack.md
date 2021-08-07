# webpack 

# what is webpack 
- it is a bundler , in bundels all files for the peoject into single file 
- takes care of the loading order of files 
- in our morders project we use es6 syntax and aslo import css and svg files in our js code , and we need to somehow import these js files in out html file .But our browsers do not support the content of the js files , so webpack comes to the rescue  
- webpack can do stuff before the file bundels and also do stuff after the files are bundeled 
- the before stuffs are like converting mordern js into browser compatible js , rsolve module loading order , loading css , svg etc files (which are done by loaders component)
- and stuff after the module bundels are like injecting the bundeled files into a html (which are done by plugins component )
## The basic components of webpack are 
- `entry` (defines the entry point) 
- `output` (defines the output dir)
- `loaders` (things to do before bundeling the files)
- `plugins` (thisng to do after bundeling the files)
- `mode` (development mode or porduction mode )

the webpack config are written usually in `webpack.config.js` file 
## sample webpack config file for react 

```
const path = require("path");
const HtmlWebpackPlugin = require("html-webpack-plugin");
module.exports = {
  entry: "./app/index.js",
  module: {
    rules: [
      {
        test: /\.svg$/,
        use: "svg-inline-loader",
      },
      {
        test: /\.css$/i,
        use: ["style-loader", "css-loader"],
      },
      {
        test: /\.(js)$/,
        use: "babel-loader",
      },
    ],
  },
  output: {
    path: path.resolve(__dirname, "dist"),
    filename: "bundle.js",
  },
  plugins: [new HtmlWebpackPlugin()],
  mode: process.env.NODE_ENV === "production" ? "production" : "development",
};

```


# config a react project with webpack from scratch 

