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
