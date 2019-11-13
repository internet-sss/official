# 概念
他的核心，webpack 对于JS应用模型是一个静态的模块打包者。
当 webpack 处理你的应用的时候，它内部构建了一个依赖图，遍历你项目需要的每一个模块的依赖图或者生成一个或更多的包。

```
更多 JavaScript 模块和 webpack 模块请查看 CONCEPTS-->Modules
```
自从 4.0.0 版本后，webpack 打包项目的时候不需要配置文件。
然而那是难以置信的对于更好的配置你的需要。
- Entry
- Output
- Loaders
- Plugins
- Mode
- Browser Compatibility

这篇文档旨在提供高级概念，同时提供详细的特定案例的链接

对于一个更好理解模块打包器背后的思想和他们如何在引擎盖下工作，查阅这些资源：
- [Manually Bundling an Application](https://www.youtube.com/watch?v=UNMkLHzofQI)
- [Live Coding a Simple Module Bundler](https://www.youtube.com/watch?v=Gc9-7PBqOC8)
- [Detailed Explanation of a Simple Module Bundler](https://github.com/ronami/minipack)


## Entry
一个入口指示器，webpack 使用哪个模块开始构建它的内部依赖图。webpack 将计算出入口点依赖哪个模块和库(直接或间接)。

他的默认值是 ./src/index.js，但是你能通过设置 webpack 一个入口配置属性设置一个不同或多个入口点，例如： webpack.config.js


webpack.config.js
```js
module.exports = {
  entry: './path/to/my/entry/file.js'
};
```

```
更多信息查看章节 CONCEPTS-->ENTRY Points
```

## Output
output 属性告诉 webpack 将打包文件放在哪和如何去命名他们。它的主要输出文件默认放在 ./dist/main.js，其他的文件放在 ./dist 目录下。

在配置文件中你可以通过 output 配置特殊的流程： webpack.config.js

webpack.config.js
```
const path = require('path');

module.exports = {
  entry: './path/to/my/entry/file.js',
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'my-first-webpack.bundle.js'
  }
};
```

```
The output property has many more configurable features. If you want to learn about the concepts behind it, you can read more in the output section.
```
在上面的例子中，我们使用 output.filename 和 output.path 属性告诉 webpack 打包后文件的名称和想要放到哪里。
在这个例子中你对于最顶部被导入的模块很好奇，它能操作文件的路径是 NodeJs module 的核心

```
output 有更多配置特征。如果你想去了解这些概念背后，你可以多读章节 CONCEPTS-->Output
```

## Loaders

在盒子外面，webpack 只能理解 JavaScript 和 JSON 文件。
Loaders 允许 webpack 去处理其他类型的文件与转变他们为被你的应用确认的有效的模块并且增加到依赖图中。

```

```

At a high level, loaders have two properties in your webpack configuration:

- The test property identifies which file or files should be transformed.
- The use property indicates which loader should be used to do the transforming.

webpack.config.js
```
const path = require('path');

module.exports = {
  output: {
    filename: 'my-first-webpack.bundle.js'
  },
  module: {
    rules: [
      { test: /\.txt$/, use: 'raw-loader' }
    ]
  }
};
```
The configuration above has defined a rules property for a single module with two required properties: test and use. This tells webpack's compiler the following:

> "Hey webpack compiler, when you come across a path that resolves to a '.txt' file inside of a require()/import statement, use the raw-loader to transform it before you add it to the bundle."

```
It is important to remember that when defining rules in your webpack config, you are defining them under module.rules and not rules. For your benefit, webpack will warn you if this is done incorrectly.
```

```
Keep in mind that when using regex to match files, you may not quote it. i.e /\.txt$/ is not the same as '/\.txt$/' or "/\.txt$/". The former instructs webpack to match any file that ends with .txt and the latter instructs webpack to match a single file with an absolute path '.txt'; this is likely not your intention.
```


```
有能力去导入任意类型的模块，例如：.css，对于 webpack 是一个特殊的特征并且可能不被其他的打包者或任务运行者支持。
我们认为这个语言的扩展是被保证的，允许开发者构建更多的准确的依赖图。
```
作为一个高版本，loaders 有两个属性在你的 webpack 配置中：
  - 1. test 属性标识哪个文件或那些文件被转换
  - 2. use 属性标识哪些 loader 应该去做转换
----

## Plugins
While loaders are used to transform certain types of modules, plugins can be leveraged to perform a wider range of tasks like bundle optimization, asset management and injection of environment variables.

```
Check out the plugin interface and how to use it to extend webpack's capabilities.
```

In order to use a plugin, you need to require() it and add it to the plugins array. Most plugins are customizable through options. Since you can use a plugin multiple times in a config for different purposes, you need to create an instance of it by calling it with the new operator.

webpack.config.js

```
const HtmlWebpackPlugin = require('html-webpack-plugin'); //installed via npm
const webpack = require('webpack'); //to access built-in plugins

module.exports = {
  module: {
    rules: [
      { test: /\.txt$/, use: 'raw-loader' }
    ]
  },
  plugins: [
    new HtmlWebpackPlugin({template: './src/index.html'})
  ]
};

```
In the example above, the html-webpack-plugin generates an HTML file for your application by injecting automatically all your generated bundles.
```
There are many plugins that webpack provides out of the box! Check out the list of plugins.
```
Using plugins in your webpack config is straightforward. However, there are many use cases that are worth further exploration. Learn more about them here.

## Mode
By setting the mode parameter to either development, production or none, you can enable webpack's built-in optimizations that correspond to each environment. The default value is production.
```
module.exports = {
  mode: 'production'
};
```
Learn more about the mode configuration here and what optimizations take place on each value.

## Browser Compatibility
webpack supports all browsers that are ES5-compliant (IE8 and below are not supported). webpack needs Promise for import() and require.ensure(). If you want to support older browsers, you will need to load a polyfill before using these expressions.
