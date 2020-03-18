## Actions
首先让我们定义一些actions（动作）。
**actions**是从应用发送信息到store（仓库）的载体。它们是store信息的*唯一*源头。使用它时你需要用到`store.dispatch()`。  
例子，添加一个新的计划项对应的action：
```
const ADD_TODO = 'ADD_TODO'

{
  type: ADD_TODO,
  text: 'Build my first Redux app'
}
```
actions是纯粹的JS对象。actions必须有`type`特性，来说明发生的action类型。types通常被定义为字符串常量。如果你的应用太大了，你一般会在不同的模组定义它。
```
import { ADD_TODO, REMOVE_TODO } from '../actionTypes'
```
> 你不一定要把type定义成不同的模组。对于小项目，你只需要把它定义成字符串。然而把type定义在其它代码文件中有一定好处。

action对象除了type之外的结构没有规定，如果乐意的话可以参考[Flux standard action](https://github.com/acdlite/flux-standard-action)。  
我们需要再加一个action type，来描述做完了的计划项。我们需要通过`index`来指向这个计划项，因为action是以数组形式储存。实践中给每一个新东西加一个独特的ID是明智的。
```
{
  type: TOGGLE_TODO,
  index: 5
}
```
每个action所传递的数据应该越少越好。例如，只传index比传整个todo对象要好。  
最后，添加一个描述能否看到计划项的action。
```
{
  type: SET_VISIBILITY_FILTER,
  filter: SHOW_COMPLETED
}
```
## Action Creators
**Action Creators**是创建action的函数。action creator容易与action混用，可以的话还是尽量正确使用这两个词。  
在Redux中，action creators会返回一个action。
```
function addTodo(text) {
  return {
    type: ADD_TODO,
    text
  }
}
```
这使其容易测试，方便移植。  
在Flux中，调用action creators经常触发dispatch（分发），像这样：
```
function addTodoWithDispatch(text) {
  const action = {
    type: ADD_TODO,
    text
  }
  dispatch(action)
}
```
Redux不是这样。如果你需要dispatch，你需要把action creators的返回值，也就是action作为参数传入`dispatch()`函数：
```
dispatch(addTodo(text))
dispatch(completeTodo(index))
```
你也可以通过创建bound action creator（创建者与分发相绑定）实现自动dispatch。
```
const boundAddTodo = text => dispatch(addTodo(text))
const boundCompleteTodo = index => dispatch(completeTodo(index))
```
这样你可以直接调用他们
```
boundAddTodo(text)
boundCompleteTodo(index)
```
`dispatch()`函数可以访问store对象来获取，就像这样`store.dispatch()`，但更常见的方法是使用react-redux的`connect()`工具。你可以使用`bindActionCreators()`绑定多个action creator至一个`dispatch()`函数。  
action creator也可以是异步的，因而有点副作用。你可以在高级教程中进行了解。
## 源代码
`actions.js`
```
/*
 * action types
 */

export const ADD_TODO = 'ADD_TODO'
export const TOGGLE_TODO = 'TOGGLE_TODO'
export const SET_VISIBILITY_FILTER = 'SET_VISIBILITY_FILTER'

/*
 * other constants
 */

export const VisibilityFilters = {
  SHOW_ALL: 'SHOW_ALL',
  SHOW_COMPLETED: 'SHOW_COMPLETED',
  SHOW_ACTIVE: 'SHOW_ACTIVE'
}

/*
 * action creators
 */

export function addTodo(text) {
  return { type: ADD_TODO, text }
}

export function toggleTodo(index) {
  return { type: TOGGLE_TODO, index }
}

export function setVisibilityFilter(filter) {
  return { type: SET_VISIBILITY_FILTER, filter }
}
```
## 下一步
创建reducer，描述应用状态变化时怎么样dispatch这些action。
