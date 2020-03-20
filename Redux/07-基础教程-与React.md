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
这些都是普通的React组件，所以我们不进行深究。我们将使用无state函数组件，直到我们需要使用本地state或生命周期方法。这不意味着展示组件必须是函数，这只是定义起来比较方便。如果你需要添加本地state，声明周期方法，或者进行优化，你可以将其转化为state组件。  
`components/Todo.js`
```
import React from 'react'
import PropTypes from 'prop-types'

const Todo = ({ onClick, completed, text }) => (
  <li
    onClick={onClick}
    style={{
      textDecoration: completed ? 'line-through' : 'none'
    }}
  >
    {text}
  </li>
)

Todo.propTypes = {
  onClick: PropTypes.func.isRequired,
  completed: PropTypes.bool.isRequired,
  text: PropTypes.string.isRequired
}

export default Todo
```
`components/TodoList.js`
```
import React from 'react'
import PropTypes from 'prop-types'
import Todo from './Todo'

const TodoList = ({ todos, onTodoClick }) => (
  <ul>
    {todos.map((todo, index) => (
      <Todo key={index} {...todo} onClick={() => onTodoClick(index)} />
    ))}
  </ul>
)

TodoList.propTypes = {
  todos: PropTypes.arrayOf(
    PropTypes.shape({
      id: PropTypes.number.isRequired,
      completed: PropTypes.bool.isRequired,
      text: PropTypes.string.isRequired
    }).isRequired
  ).isRequired,
  onTodoClick: PropTypes.func.isRequired
}

export default TodoList
```
`components/Link.js`
```
import React from 'react'
import PropTypes from 'prop-types'

const Link = ({ active, children, onClick }) => {
  if (active) {
    return <span>{children}</span>
  }

  return (
    <a
      href=""
      onClick={e => {
        e.preventDefault()
        onClick()
      }}
    >
      {children}
    </a>
  )
}

Link.propTypes = {
  active: PropTypes.bool.isRequired,
  children: PropTypes.node.isRequired,
  onClick: PropTypes.func.isRequired
}

export default Link
```
`components/Footer.js`
```
import React from 'react'
import FilterLink from '../containers/FilterLink'
import { VisibilityFilters } from '../actions'

const Footer = () => (
  <p>
    Show: <FilterLink filter={VisibilityFilters.SHOW_ALL}>All</FilterLink>
    {', '}
    <FilterLink filter={VisibilityFilters.SHOW_ACTIVE}>Active</FilterLink>
    {', '}
    <FilterLink filter={VisibilityFilters.SHOW_COMPLETED}>Completed</FilterLink>
  </p>
)

export default Footer
```
### 实现容器组件
好，现在可以将这些展示组件通过容器组件挂到Redux上。技术上，容器组件是一种使用了[store.subscribe()](https://redux.js.org/api/store#subscribelistener)的React组件，用以读取Redux的state树，给它渲染的展示组件提供props。还是那句话，你可以手写容器组件，但我们建议使用React Redux库的[connect()](https://react-redux.js.org/using-react-redux/connect-mapstate)方法，可以提供很多性能优化，避免不必要的渲染。（有点之一是你不要再担心自己取实现[React性能建议](https://facebook.github.io/react/docs/advanced-performance.html)中的`shouldComponentUpdate`）。  
要用到`connect`，你需要定义一个特殊的函数叫做`mapStateToProps`，用于将当前Redux store中的state作为props传入容器中的展示组件。例如，`VisibleTodoList`这个容器组件需要计算`todos`，并传入`Todolist`这个展示组件，因而我们定义一个根据`state.visibilityFilter`过滤`state.todos`的函数，在`mapStateToProps`函数中使用它：
```
const getVisibleTodos = (todos, filter) => {
  switch (filter) {
    case 'SHOW_COMPLETED':
      return todos.filter(t => t.completed)
    case 'SHOW_ACTIVE':
      return todos.filter(t => !t.completed)
    case 'SHOW_ALL':
    default:
      return todos
  }
}

const mapStateToProps = state => {
  return {
    todos: getVisibleTodos(state.todos, state.visibilityFilter)
  }
}
```
除了读取state，容器组件也能dispatch actions。类似的，你可以定义一个叫做`mapDispatchToProps()`的函数，以`dispatch()`方法作为参数，返回你想要注入展示组件的回调props。例如，我们想让`VisibleTodoList`这个容器组件发射一个叫做`onTodoClick`的prop，注入`TodoList`展示组件，我们也想要`onTodoClick`dispatch一个叫`TOGGLE_TODO`的action：
```
const mapDispatchToProps = dispatch => {
  return {
    onTodoClick: id => {
      dispatch(toggleTodo(id))
    }
  }
}
```
最后，我们通过调用`connect()`并传入上述两个函数创建`VisibleTodoList`这个容器组件：
```
import { connect } from 'react-redux'

const VisibleTodoList = connect(mapStateToProps, mapDispatchToProps)(TodoList)

export default VisibleTodoList
```
这些是React Redux API的基础，但这里还有些简短有力的选项，所以我们建议你去详细核对[其文档](https://github.com/reduxjs/react-redux)。比如你担心`mapStateToProps`创建了太多的新对象， 你可以去学习[reselect](https://github.com/reduxjs/reselect)来[计算取得的数据](https://redux.js.org/recipes/computing-derived-data)。  
下面是其它容器组件：  
`containers/FilterLink.js`
```
import { connect } from 'react-redux'
import { setVisibilityFilter } from '../actions'
import Link from '../components/Link'

const mapStateToProps = (state, ownProps) => {
  return {
    active: ownProps.filter === state.visibilityFilter
  }
}

const mapDispatchToProps = (dispatch, ownProps) => {
  return {
    onClick: () => {
      dispatch(setVisibilityFilter(ownProps.filter))
    }
  }
}

const FilterLink = connect(mapStateToProps, mapDispatchToProps)(Link)

export default FilterLink
```
`containers/VisibleTodoList.js`
```
import { connect } from 'react-redux'
import { toggleTodo } from '../actions'
import TodoList from '../components/TodoList'

const getVisibleTodos = (todos, filter) => {
  switch (filter) {
    case 'SHOW_ALL':
      return todos
    case 'SHOW_COMPLETED':
      return todos.filter(t => t.completed)
    case 'SHOW_ACTIVE':
      return todos.filter(t => !t.completed)
  }
}

const mapStateToProps = state => {
  return {
    todos: getVisibleTodos(state.todos, state.visibilityFilter)
  }
}

const mapDispatchToProps = dispatch => {
  return {
    onTodoClick: id => {
      dispatch(toggleTodo(id))
    }
  }
}

const VisibleTodoList = connect(mapStateToProps, mapDispatchToProps)(TodoList)

export default VisibleTodoList
```
## 实现其它组件
`containers/AddTodo.js`  
回忆一下之前提到的，`AddTodo`组件的展示和逻辑混合到了同一个定义中。
```
import React from 'react'
import { connect } from 'react-redux'
import { addTodo } from '../actions'

let AddTodo = ({ dispatch }) => {
  let input

  return (
    <div>
      <form
        onSubmit={e => {
          e.preventDefault()
          if (!input.value.trim()) {
            return
          }
          dispatch(addTodo(input.value))
          input.value = ''
        }}
      >
        <input
          ref={node => {
            input = node
          }}
        />
        <button type="submit">Add Todo</button>
      </form>
    </div>
  )
}
AddTodo = connect()(AddTodo)

export default AddTodo
```
如果你不熟悉`ref`属性，请阅读这份[文档](https://facebook.github.io/react/docs/refs-and-the-dom.html)来正确使用它。
### 将容器组件合起来
`components/App.js`
```
import React from 'react'
import Footer from './Footer'
import AddTodo from '../containers/AddTodo'
import VisibleTodoList from '../containers/VisibleTodoList'

const App = () => (
  <div>
    <AddTodo />
    <VisibleTodoList />
    <Footer />
  </div>
)

export default App
```
## 传Store。
所有容器组件都需要访问Redux store来订阅它。一种方法是将它传给每个容器组件。但这样太烦了，你甚至需要传给展示组件，因为它偶尔会渲染组件中的某个容器。  
我们建议的方法是使用一个特殊的React Redux组件，叫做<Provider>。使其包含的组件都能获取store而不用显性传入。你只需要在渲染它的根组件中使用一次。  
  `index.js`
```
import React from 'react'
import { render } from 'react-dom'
import { Provider } from 'react-redux'
import { createStore } from 'redux'
import todoApp from './reducers'
import App from './components/App'

const store = createStore(todoApp)

render(
  <Provider store={store}>
    <App />
  </Provider>,
  document.getElementById('root')
)
```
