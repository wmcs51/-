![reducer](https://images-na.ssl-images-amazon.com/images/I/A1edVtIyS2L._SX342_.jpg)  
Reducer确立应用state（状态）发生变化时，action怎么样发送数据至store。记住action只描述发生过了什么，不描述应用state怎么变。
## 设计state结构
在Redux中，所有应用的state都存在一个单一的对象中。所以写点代码之前最好考虑下结构。怎样以最小的表现形式来描述你应用的state？  
对我们的todo应用来说，我们需要存两样东西:
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
