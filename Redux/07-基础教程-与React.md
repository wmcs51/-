在最开始我们需要申明Redux和React没关系。你可以和React, Angular, Ember, jQuery一起使用Redux应用，甚至是单纯的JavaScript。  
通常来说，Redux在类似React和Deku的库下工作的比较好，因为它们通过state的函数描述UI，而Redux会通过action更新state。  
我们将使用React来写我们的todo应用，并覆盖与React一起使用Redux的基础知识。
> 你可以在[**React-Redux官方文档**](https://react-redux.js.org/)上看到完整的指导。

## 安装React-Redux
React绑定并不默认包含在Redux中。你需要手动安装。
```
npm install react-redux
```
你也可以使用UMD包（[测试](https://unpkg.com/react-redux@latest/dist/react-redux.js)环境或[生产](https://unpkg.com/react-redux@latest/dist/react-redux.min.js)环境都可以）。UMD包会输出一个`window.ReactRedux`的全局对象，只要加到你的网页`<script>`标签中。
## 展示组件和容器组件
React Redux绑定会区分*presentational展示*组件和*container容器*组件。这将使你的应用更容易理解和复用。下面将展示组件和容器组件的区别（如果你不熟悉的话，我们建议你阅读这篇[文章](https://medium.com/@dan_abramov/smart-and-dumb-components-7ca2f9a7c7d0)）:
||展示组件|容器组件|
|-|-|-|
|目的|事物是什么样子（标记，样式）|事物怎么运行（数据流，state更新）|
|感知Redux|不能|可以|
|怎么读数据|从props中读|需要从Redux state中订阅|
|改变数据|调用props中的回调|dispatch Redux actions|
|怎么写的|手写|通常由React Redux生成|
