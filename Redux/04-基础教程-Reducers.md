![reducer](https://images-na.ssl-images-amazon.com/images/I/A1edVtIyS2L._SX342_.jpg)  
Reducer确立应用state（状态）发生变化时，action怎么样发送数据至store。记住action只描述发生过了什么，不描述应用state怎么变。
## 设计state结构
在Redux中，所有应用的state都存在一个单一的对象中。所以写点代码之前最好考虑下结构。怎样以最小的表现形式来描述你应用的state？  
对我们的todo应用来说，我们需要存两样东西：
- 当前选择的visibility filter（可见性过滤器）
- 实际的计划项列表

你常需要存一些数据以及UI状态至state树。这很正常，不过最好将数据和UI状态分离。
```
{
  visibilityFilter: 'SHOW_ALL',
  todos: [
    {
      text: 'Consider using Redux',
      completed: true
    },
    {
      text: 'Keep all state in a single tree',
      completed: false
    }
  ]
}
```
> 在更复杂的应用中，你需要不同的实体互相访问。我们建议将你的state尽可能不要有嵌套。保证每个对象中的实体有一个ID作为键值，用这个ID来指向这个实体。
这种方法在[普通化](https://github.com/paularmstrong/normalizr)文档中有具体描述。比如示例应用中，在state中设置`todosById: { id -> todo }`和
`todos: array<id>`会更好，但在这个教程中我们希望描述得尽可能简单一些。
## 着手处理actions
现在我们已经决定好state对象长什么样了，是时候写个reducer了。reducer是一个纯粹的函数，它取之前的state和一个action作为参数，返回之后的state。
```
(previousState, action) => nextState
```
被称作reducer是因为它需要作为参数传向`Array.prototype.reduce(reducer, ?initialValue)`。reducer必须是纯粹的函数。你不应该在reducer中做下面这些事情：
- 替换实参（argument）
- 进行有副作用的操作，比如调用API，网页路径变换
- 调用不纯粹的函数，比如`Date.now()``Math.random()`

我们之后将探索怎么样进行有副作用的操作。现在，只要记住reducer必须是纯粹的。
**给定一个实参，它需要计算并返回之后的state。没有惊喜，没有副作用，没有调用API，没有替换实参。只是做了计算**。  
懂了这点之后，我们将开始用之前写的action来学写reducer。  
首先明确初始state。Redux初次调用reducer时state默认为`undefined`。这是我们返回应用初始state的机会。
```
import { VisibilityFilters } from './actions'

const initialState = {
  visibilityFilter: VisibilityFilters.SHOW_ALL,
  todos: []
}

function todoApp(state, action) {
  if (typeof state === 'undefined') {
    return initialState
  }

  // For now, don't handle any actions
  // and just return the state given to us.
  return state
}
```
一个小技巧能使代码更简洁紧凑，ES6默认实参句法（default arguments syntax）：
```
function todoApp(state = initialState, action) {
  // For now, don't handle any actions
  // and just return the state given to us.
  return state
}
```
接下来这步将处理`SET_VISIBILITY_FILTER`。要做的是改变state中`visibilityFilter`。简单：
```
import {
  SET_VISIBILITY_FILTER,
  VisibilityFilters
} from './actions'

...

function todoApp(state = initialState, action) {
  switch (action.type) {
    case SET_VISIBILITY_FILTER:
      return Object.assign({}, state, {
        visibilityFilter: action.filter
      })
    default:
      return state
  }
}
```
注意：  
1. **我们没有替换`state`**。我们通过 `Object.assign()`创建了一份拷贝。
`Object.assign(state, { visibilityFilter: action.filter })`也是错误的。它会替换第一个实参。你**必须**提供一个空对象作为第一个形参。
你也可以用展开操作符（object spread operator），像这样`{ ...state, ...newState }`写代码。
2. **在默认情形下我们返回了前一个state**。对于任何一个未知的action来说，必须返回前一个state。
> `Object.assign()`属于ES6，不被老的浏览器支持。要支持老的浏览器，你可以选择使用polyfill（多补，多版本兼容工具），也就是[Bable插件](https://www.npmjs.com/package/babel-plugin-transform-object-assign)，或者其它库的工具，比如[_.assign()](https://lodash.com/docs#assign)。

>**`switch`和Boilerplate**  
`switch`申明不是真的boilerplate（铸模）。Flux的boilerplate是概念性的：需要发射一个更新，需要用Dispatcher在Store中注册，需要Store为一个对象（以及跨平台需求带来的棘手问题）。Redux使用纯粹的reducer解决了这些问题。  
不幸的是许多人还是根据是否使用`switch`声明来选择框架。如果你不喜欢`switch`，你可以用`createReducer`函数来接受匹配处理（handler map），详见[reducing boilerplate](https://redux.js.org/recipes/reducing-boilerplate#reducers)。
## 处理更多actions
我们还剩两个actions要处理！就像我们对`SET_VISIBILITY_FILTER`做的那样，我们将引入`ADD_TODO`和`TOGGLE_TODO`这两个actions，然后拓展我们的reducer来处理`ADD_TODO`。
```
import {
  ADD_TODO,
  TOGGLE_TODO,
  SET_VISIBILITY_FILTER,
  VisibilityFilters
} from './actions'

...

function todoApp(state = initialState, action) {
  switch (action.type) {
    case SET_VISIBILITY_FILTER:
      return Object.assign({}, state, {
        visibilityFilter: action.filter
      })
    case ADD_TODO:
      return Object.assign({}, state, {
        todos: [
          ...state.todos,
          {
            text: action.text,
            completed: false
          }
        ]
      })
    default:
      return state
  }
}
```
就像之前那样，我们不要直接写state值或作用域（fields），而是返回一个新的对象。新`todos`将是旧`todos`与新计划项的级联。action中的数据构成了更新后的todo。  
最后，`TOGGLE_TODO`的实现不该是个意外了吧：
```
case TOGGLE_TODO:
  return Object.assign({}, state, {
    todos: state.todos.map((todo, index) => {
      if (index === action.index) {
        return Object.assign({}, todo, {
          completed: !todo.completed
        })
      }
      return todo
    })
  })
```
因为我们想要更新数组中特定的项而不寻求替换，我们得创建一个有相同项的新数组，除了那个在action中指定了索引的项。如果你发现你经常写这种操作，可以尝试取用些帮助工具比如[immutability helper](https://github.com/kolodny/immutability-helper)，[updeep](https://github.com/substantial/updeep)，甚至是原生支持深度更新的库比如[immutable](http://facebook.github.io/immutable-js/)。总之要记住在拷贝`state`之前不要往里面塞东西。
## 分割Reducers
下面是目前的代码，并不烦：
```
function todoApp(state = initialState, action) {
  switch (action.type) {
    case SET_VISIBILITY_FILTER:
      return Object.assign({}, state, {
        visibilityFilter: action.filter
      })
    case ADD_TODO:
      return Object.assign({}, state, {
        todos: [
          ...state.todos,
          {
            text: action.text,
            completed: false
          }
        ]
      })
    case TOGGLE_TODO:
      return Object.assign({}, state, {
        todos: state.todos.map((todo, index) => {
          if (index === action.index) {
            return Object.assign({}, todo, {
              completed: !todo.completed
            })
          }
          return todo
        })
      })
    default:
      return state
  }
}
```
有更容易理解代码的方法嘛？看上去`todos`和`visibilityFilter`是完全独立更新的。有时候state作用域有相互依赖，但在我们的例子中我们可以很容易将`todos`更新分离到新的函数中：
```
function todos(state = [], action) {
  switch (action.type) {
    case ADD_TODO:
      return [
        ...state,
        {
          text: action.text,
          completed: false
        }
      ]
    case TOGGLE_TODO:
      return state.map((todo, index) => {
        if (index === action.index) {
          return Object.assign({}, todo, {
            completed: !todo.completed
          })
        }
        return todo
      })
    default:
      return state
  }
}

function todoApp(state = initialState, action) {
  switch (action.type) {
    case SET_VISIBILITY_FILTER:
      return Object.assign({}, state, {
        visibilityFilter: action.filter
      })
    case ADD_TODO:
      return Object.assign({}, state, {
        todos: todos(state.todos, action)
      })
    case TOGGLE_TODO:
      return Object.assign({}, state, {
        todos: todos(state.todos, action)
      })
    default:
      return state
  }
}
```
注意`todos`也接受`state`——但是`state`是个数组！现在`todoApp`让`todos`管理一部分`state`，而且`todos`知道怎么管理。**这叫做*reducer composition*，这是构建Redux应用的基础流程**。  
让我们更多地了解reducer composition。我们可以抽离一个reducer只管理`visibilityFilter`嘛？可以。  
在下面的引用中，让我们使用[ES6解构](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment)来声明`SHOW_ALL`：
```
const { SHOW_ALL } = VisibilityFilters
```
然后：
```
function visibilityFilter(state = SHOW_ALL, action) {
  switch (action.type) {
    case SET_VISIBILITY_FILTER:
      return action.filter
    default:
      return state
  }
}
```
现在我们可以重写主reducer，将其作为一个调用其它部分管理state的reducer的函数。现在也不需要知道所有初始的state。因为当state参数为undefined时，每个子reducers都会返回初始state。
```
function todos(state = [], action) {
  switch (action.type) {
    case ADD_TODO:
      return [
        ...state,
        {
          text: action.text,
          completed: false
        }
      ]
    case TOGGLE_TODO:
      return state.map((todo, index) => {
        if (index === action.index) {
          return Object.assign({}, todo, {
            completed: !todo.completed
          })
        }
        return todo
      })
    default:
      return state
  }
}

function visibilityFilter(state = SHOW_ALL, action) {
  switch (action.type) {
    case SET_VISIBILITY_FILTER:
      return action.filter
    default:
      return state
  }
}

function todoApp(state = {}, action) {
  return {
    visibilityFilter: visibilityFilter(state.visibilityFilter, action),
    todos: todos(state.todos, action)
  }
}
```
**注意每个reducers都管理自己的那部分全局state。`state`参数对于每个reducer都是不同的，只对应其管理的那部分。**  
这看起来已经很棒了！当应用变庞大时，我们可以将reducers拆分到不同文件中，使它们完全独立，只管理自己那部分。  
最后，Redux提供了一个叫[combineReducers()](https://redux.js.org/api/combinereducers)的实用程序，和上面的`todoApp`函数逻辑类似。有了这个程序后，我们可以像这样重写`todoApp`：
```
import { combineReducers } from 'redux'

const todoApp = combineReducers({
  visibilityFilter,
  todos
})

export default todoApp
```
这和下面的代码是等价的：
```
export default function todoApp(state = {}, action) {
  return {
    visibilityFilter: visibilityFilter(state.visibilityFilter, action),
    todos: todos(state.todos, action)
  }
}
```
你可以给他们不同的键值，或者调用不同的函数。这两种方式写组合reducer是等价的：
```
const reducer = combineReducers({
  a: doSomethingWithA,
  b: processB,
  c: c
})
```
```
function reducer(state = {}, action) {
  return {
    a: doSomethingWithA(state.a, action),
    b: processB(state.b, action),
    c: c(state.c, action)
  }
}
```
