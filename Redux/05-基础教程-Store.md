前几节中，我们定义了action，表示了发生了什么。也定义了reducer，表示发生这些actions时怎么样更新state。
**Store**是将这些组合起来的对象。store有这些责任：
- 保存应用state
- 允许通过[`getState()`](https://redux.js.org/api/store#getState)访问state
- 允许通过[`dispatch(action)`](https://redux.js.org/api/store#dispatchaction)更新state
- 通过[`subscribe(listener)`](https://redux.js.org/api/store#subscribelistener)注册监听（register listener）
- 通过[`subscribe(listener)`](https://redux.js.org/api/store#subscribelistener)返回的函数处理未注册的监听

需要注意的是在一个Redux应用中只能有一个store。当你需要拆分你的数据处理逻辑，你得使用[reducer composition](https://redux.js.org/basics/reducers#splitting-reducers)而不是多个store。  
如果你有reducer创建store会是简单的。在上节中，我们使用了[`combineReducers()`](https://redux.js.org/api/combinereducers)来组合多个reducer。我们现在将引入它，并将其传入[`createStore()`](https://redux.js.org/api/createstore)。
```
import { createStore } from 'redux'
import todoApp from './reducers'
const store = createStore(todoApp)
```
[`createStore()`](https://redux.js.org/api/createstore)的第二个参数是可选的初始state。这对客户端的state与服务器Redux应用的state相匹配有很大作用。
```
const store = createStore(todoApp, window.STATE_FROM_SERVER)
```
## Dispatching Actions
现在我们创建了一个store，让我们确定程序能不能跑！就算还没UI，我们已经可以测试更新逻辑。
```
import {
  addTodo,
  toggleTodo,
  setVisibilityFilter,
  VisibilityFilters
} from './actions'

// Log the initial state
console.log(store.getState())

// Every time the state changes, log it
// Note that subscribe() returns a function for unregistering the listener
const unsubscribe = store.subscribe(() => console.log(store.getState()))

// Dispatch some actions
store.dispatch(addTodo('Learn about actions'))
store.dispatch(addTodo('Learn about reducers'))
store.dispatch(addTodo('Learn about store'))
store.dispatch(toggleTodo(0))
store.dispatch(toggleTodo(1))
store.dispatch(setVisibilityFilter(VisibilityFilters.SHOW_COMPLETED))

// Stop listening to state updates
unsubscribe()
```
你可在控制台看到这些操作怎样改变了store中的state：  
![console](https://i.imgur.com/zMMtoMz.png)
我们在写UI之前明确了应用的行为。在教程中不会做这些测试，不过你可以自己试着去做。调用它们，并判定发生了啥。
## 源代码
`index.js`
```
import { createStore } from 'redux'
import todoApp from './reducers'

const store = createStore(todoApp)
```
## 下一步
在为todo应用创建UI之前，我们需要先看下Redux应用的数据流向。
