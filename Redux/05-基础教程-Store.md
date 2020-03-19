前几节中，我们定义了action，表示了发生了什么。也定义了reducer，表示发生这些actions时怎么样更新state。
**Store**是将这些组合起来的对象。store有这些责任：
- 保存应用state
- 允许通过`[getState()](https://redux.js.org/api/store#getState)`访问state
- 允许通过`[dispatch(action)](https://redux.js.org/api/store#dispatchaction)`更新state
- 通过`[subscribe(listener)](https://redux.js.org/api/store#subscribelistener)`注册监听（register listener）
- 通过`[subscribe(listener)](https://redux.js.org/api/store#subscribelistener)`返回的函数处理未注册的监听
需要注意的是在一个Redux应用中只能有一个store。当你需要拆分你的数据处理逻辑，你得使用[reducer composition](https://redux.js.org/basics/reducers#splitting-reducers)而不是多个store。  
如果你有reducer创建store会是简单的。在上节中，我们使用了[combinereducers()](https://redux.js.org/api/combinereducers)来组合多个reducer。我们现在将引入它，并将其传入[createStore()](https://redux.js.org/api/createstore)
