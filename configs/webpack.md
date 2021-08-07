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
  output: {
    path: path.resolve(__dirname, "dist"),
    filename: "bundle.js",
  },
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

  plugins: [new HtmlWebpackPlugin()],
  mode: process.env.NODE_ENV === "production" ? "production" : "development",
};

```
the webpack config file is a simple js file which exports an object . 
in the above file the entry and output attribute are quite clear .

## loaders 
( loaders are things that need to be processed or loaded before the actual bundeling starts) in the module attributes rules array . for a loader entry the targeted files are selected by the test attribute and the loader through the use attribute 
```
 {
     test : \targetted-files\ 
     use :  loader-to-be-used
 }
```
hear we want to load svg (svg-inline-loader), css ("style-loader", "css-loader") and and transpile out es6 code the vanilla javascript (babel-loader) 

we can use multiple loaders as we can see for css the style-loader is dependent on css-loader . the loading order of the loaders are form the right so css-loader will load first 
and style-loader will load later 
note that all the loaders and plugins are node modules 
we can also exclude files or folders in loader 

```
{
    test: /\.(js)$/,
    use: "babel-loader",
    exclude: "node_modules" ,
}
```
this will exclude the node_modules folder from being transpiled 
## plugins 
plugins attribute takes in a array of plugins ,in the above file  `HtmlWebpackPlugin` plugin inject the bundeled files in an html file in the output dir otherwise we would have to crate it manually 
# config a react project with webpack from scratch 

