# webpack-react-setup
### Ania Kubow - youtube tutorial 
[https://www.youtube.com/watch?v=G76SICBNSfs](https://www.youtube.com/watch?v=G76SICBNSfs)

## open terminal

`$`
```
    mkdir react-setup
    cd react-setup
    touch package.json
    npm init
```

## Webpack 

- webpack-cli // the terminal commands we need
- webpack-dev-server // a package that will watch for changes
- html-webpack-plugin // this will allow webpack to add script tags to html
```
    npm install webpack webpack-cli webpack-dev-server html-webpack-plugin
```
## Babel

- is a JavaScript compiler used to convert code into a backwards compatible version of javascript in current and old browsers or environments
- babel plugins are used to transform syntax that is not widely supported into a backwards compatible version
- for example arrow functions which are specified in es6 are converted into regular function declarations

`$`
```
    npm install @babel/core @babel/preset-env @babel/preset-react
    
    touch .babelrc
```

`.babelrc`
```
    {
      "preset": ["@babel/preset-env", "@babel/preset-react"]
    }
```
now add loaders and support for all various types of files we will use

`$`
```
    npm install babel-loader style-loader css-loader sass-loader
```

and if we want to use scss install this scss to css compiler 
```
    npm install node-sass
```
now everything is installed, 

we need to do some folder organisation and  configuration
```
    touch webpack.config.js
```

`webpack.config.js`
```
    const path = require('path')
    const webpack = require('webpack')
    const HtmlWebpackPlugin = require('html-webpack-plugin')
    
    module.exports = {
      entry: './src/app.js',
      output: {
        path: path.resolve('dist'),
        filename: 'bundle.js'
      },
      devtool: 'source-maps',
      module: {
        rules: [
          { test: /\.jsx?$/, loader: 'babel-loader', exclude: /node_modules/ },
          { test: /\.css$/, loader: ['style-loader', 'css-loader'] },
          { test: /\.s(a|c)ss$/, loader: ['style-loader', 'css-loader', 'sass-loader'] }
        ]
      },
      devServer: {
        contentBase: path.resolve('src'),
        hot: true,
        open: true,
        port: 8000,
        watchContentBase: true
      },
      plugins: [
        new webpack.HotModuleReplacementPlugin(),
        new HtmlWebpackPlugin({
          template: 'src/index.html',
          filename: 'index.html',
          inject: 'body'
        })
      ]
    }
```
or you can find & copy/paste this file from... [here](https://github.com/kubowania/React-app-setup/blob/master/webpack.config.js)



## Standard Practice

- alll the code we write needs to be compiled somewhere
- the compiled code will ultimately get sent to the browser
- the course code will not
- for this reason, we need to keep our source code and compiled code SEPERATE
- /src folder for our code
- /dist folder for compiled code

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e5784e56-d14f-448c-aafd-c61fa540f5b3/Screen_Shot_2020-03-25_at_20.12.53.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e5784e56-d14f-448c-aafd-c61fa540f5b3/Screen_Shot_2020-03-25_at_20.12.53.png)

```
add 
index.js
/dist folder 
/src folder with
  - index.html
  - style.css
  - app.js
```


for our project to run is add some scripts to test, serve & build our project

`package.json`
```
    "scripts": {
        "serve": "webpack-dev-server --mode=development",
        "build": "webpack -p"
      }, 
```

`$`
```
    npm run serve
```
 

to compile the project

`$`
```
    npm run build
```    
    
