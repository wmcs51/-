在最开始我们需要申明Redux和React没关系。你可以和React, Angular, Ember, jQuery一起使用Redux应用，甚至是单纯的JavaScript。  
通常来说，Redux在类似React和Deku的库下工作的比较好，因为它们通过state的函数描述UI，而Redux会通过action更新state。  
我们将使用React来写我们的todo应用，并覆盖与React一起使用Redux的基础知识。
> 你可以在[**React-Redux官方文档**](https://react-redux.js.org/)上看到完整的指导。

## 安装React-Redux
React绑定并不默认包含在Redux中。你需要手动安装。
```
npm install react-redux
```
你也可以使用UMD包（[测试](https://unpkg.com/react-redux@latest/dist/react-redux.js)环境或[生产](https://unpkg.com/react-redux@latest/dist/react-redux.min.js)环境都可以）。UMD包会输出一个`window.ReactRedux`的全局对象，只要把包加到你的网页`<script>`标签中。
## 展示组件和容器组件
React Redux绑定会区分*presentational展示*组件和*container容器*组件。这将使你的应用更容易理解和复用。下面将展示组件和容器组件的区别（如果你不熟悉的话，我们建议你阅读这篇[文章](https://medium.com/@dan_abramov/smart-and-dumb-components-7ca2f9a7c7d0)）:
||展示组件|容器组件|
|-|-|-|
|目的|事物是什么样子（标记，样式）|事物怎么运行（数据流，state更新）|
|感知Redux|不能|可以|
|怎么读数据|从props中读|需要从Redux state中订阅|
|改变数据|调用props中的回调|dispatch Redux actions|
|怎么写的|手写|通常由React Redux生成|

我们写的大多数组件都会是展示性的，但我们也需要写点容器组件，通过它们链接Redux store。下面的设计概要并不意味着容器组件需要接近容器树的上层。如果一个容器组件变得过于复杂（比如重度嵌套了传入很多回调的展示组件），可像[问答](https://redux.js.org/faq/react-redux#should-i-only-connect-my-top-component-or-can-i-connect-multiple-components-in-my-tree)中一样在组件树中引入另一个容器组件。  
原理上你可以自己写容器组件，通过使用[store.subscribe()](https://redux.js.org/api/store#subscribelistener)。我们不建议这样做，因为React Redux做了很多靠手写代码没法完成的性能优化。因此，与其手写容器组件，我们会通过React Redux提供的[connect()](https://react-redux.js.org/api/connect#connect)函数生成它，你将在下文中看到。
## 设计组件层级
还记得怎样设计根state对象嘛？是时候设计UI层级来匹配它。这不是Redux该完成的任务。[以React思考](https://facebook.github.io/react/docs/thinking-in-react.html)将是解释这个过程的绝佳教程。
我们的设计概要很简单。我们想要展示一列todo项。点一下，todo项就会被划去，表示完成了。我们想要一个输入框，用户可以输入新的todo项。在底部，我们想要展示一个功能键，来展示所有，或者完成了的，或者有效的todo项。
### 设计展示组件
下面的列表是我需要的展示组件,其中子列表是组件的props：
* `TodoList`展示可视todo的列表
  - `todo: Array`是todo项的数组，{id，text, completed}这样表示
  - `onTodoClick(id: number)`是点击todo项时触发的回调
* `Todo`是单一todo项。
  - `text: string`是展示的文本
  - `completed: boolean`是todo项是否进行展示的布尔值
  - `onClick()`是点击todo项时触发的回调
* `Link`是带有回调的连接
  - `onClick()`是点击link时触发的回调
* `Footer`是让用户改变可视todo项的区域
* `App`是根组件，渲染所有东西

它们描述长什么样但是不知道数据从哪来怎么改。它们只渲染给它们的。如果你将这些组件从Redux中移植出去，它们的还是会有相同的表现。它们不依赖Redux。
### 设计容器组件
我们也需要一些容器组件将展示组件连接到Redux。例如，展示性的`TodoList`组件需要像`VisibleTodoList`这样的容器来订阅Redux store，以获知如何应用当前的可视设定。为改变可视设定，我们将提供一个`FilterLink`的容器组件，来渲染一个点击后dispatch action的`Link`组件：
- `VisibleTodoList`根据当前的可视设定过滤todo项，并渲染`TodoList`
- `FilterLink`获取当前的可视设定，渲染一个`Link`。
  * `filter:string`表示可视设定。
  
### 设计其它组件
有时候可能理不清一个组件是展示型还是容器型。例如，有时候列表和函数深度组合，例如下面的小组件：
- `addTodo`是带有一个“Add”按钮的输入
技术上我们可以把它拆分成两个组件，但现在讲这个还有点早。在一个小组件上混淆展示型还是容器型没什么大不了。当它开始变大时，就有必要拆分了，先不管。
## 实现组件
让我们写这些组件！先从展示组件开始，它暂时不需要绑定Redux。
### 实现展示组件
