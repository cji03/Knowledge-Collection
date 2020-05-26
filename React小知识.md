### React

1. 由React自身控制的事件处理函数中，`this.setstate()`并不会立即执行更新操作，而是会放入更新队列中（异步，合并更新）。如果是在`addEventListener`或者是`setTimeout/setInterval`中的`setstate`操作会立即执行更新操作。（React自身事件处理函数/生命周期函数触发时会赋值`isBatchingUpdates`为`true`，此时不直接执行更新state）
2. 不影响页面UI的数据可以不用放到state中，可以放到this中。
3. React Virtual DOM, Diff 算法等。
4. React 合成事件（SyntheticEvent）; 对浏览器原生事件的包装，做了夸平台兼容处理。将所有React事件注册在`document`上，并在冒泡/捕获阶段做统一处理并分发执行回调函数。

#### componentWillMount:

- `render()` 会在 `componentWillMount` 执行后立即执行，如果写一些同步代码定义的初始变量，完全可以写在constructor中；
- 如果是异步api调用，`render()` 并不会等待异步结果返回，所以还是需要定义好初始变量，然后等待数据返回后再次`render()`，`render()`还是会被执行两次。
- 所以相关api操作，可以放至`componentDidMount`中。
-  often misused and not in line with the upcoming feature of async rendering. These cause unnecessary multiple time component re-rendering which hampers the performance.

#### pureComponent

The major difference between React.PureComponent and React.Component is PureComponent does a shallow comparison on state change. It means that when comparing scalar values it compares their values, but when comparing objects it compares only references. It helps to improve the performance of the app.

### Redux

redux-thunk中间件实现异步dispatch，使得dispatch可以接受异步函数。

Redux和service worker结合，可以将复杂的数据计算逻辑放在service worker中处理，防止阻塞。
