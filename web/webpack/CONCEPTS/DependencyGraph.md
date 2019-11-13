Any time one file depends on another, webpack treats this as a dependency. This allows webpack to take non-code assets, such as images or web fonts, and also provide them as dependencies for your application.

When webpack processes your application, it starts from a list of modules defined on the command line or in its config file. Starting from these [entry points](https://webpack.js.org/concepts/entry-points/), webpack recursively builds a dependency graph that includes every module your application needs, then bundles all of those modules into a small number of bundles - often, just one - to be loaded by the browser.

```
Bundling your application is especially powerful for HTTP/1.1 clients, 
as it minimizes the number of times your app has to wait while the browser starts a new request. 
For HTTP/2, you can also use Code Splitting to achieve best results.
```

一个文件依赖另一个文件，webpack 将其当作依赖项处理。
这就允许 webpack 获取非代码资源，例如图片或 web 字体，同时将它们作为依赖项提供给你的应用。
当 webpack 处理你的应用时，它从一个被定义在命令行的或者它的配置文件列表模块开始。从这些入口点开始，webpack 递归的构建一个依赖图，包括应用需求的每一个模块的依赖图，然而构建的那些模块被放到少数的构建文件中，通常只有一个，被浏览器加载的文件
```

对于客户端请求 HTTP/1.1 打包应用是非常有力的，当浏览器开启一个新的请求时它可以将等待倍数降到最低。
对于 HTTP/2 你也可以通过代码分割去达到最好的结果。
```