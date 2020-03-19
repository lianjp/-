## react框架相关

`备注： + 代表被问到的次数，没有 + 代表自己整理了，但没被问到`

### 生命周期+++

#### 1.组件第一次被创建渲染

###### 老版本

```javascript
constructor()   //调用构造函数
componentWillMount()  //以后要废弃
render()
componentDidMount()
```

##### 新版本

```javascript
constructor()  //调用构造函数
static getDerivedStateFromProps()  //新增生命周期函数，从props计算出来的状态
render()  //将虚拟dom渲染上去
componentDidMount()  //发送请求，拿数据 常用生命周期函数
```

#### 2.组件已经渲染后，数据更新

###### 老版本

```javascript
父元素 render()
componentWillReceiveProps()  //以后要废弃
sholdComponentUpdate()
componentWillUpdate()  //以后要废弃
render()
componentDidUpdate()
```

#####新版本

```javascript
static getDerivedStateFromProps()  //新增生命周期函数，重新从props计算出来新的状态
shouldComponentUpdate()  //判断要不要更新  更新返回true 不更新返回false 优化方面
render()  //将虚拟dom渲染上去
getSnapshotBeforeUpdata()  //新增生命周期函数   可以用来拿到dom更新之前的一些信息
componentDidUpdate()
```

#### 3.组件卸载时

```javascript
componentWillUnmount()
```

---



##### 生命周期新旧的差异

  因为react16引入了feber架构，老的生命周期对其不太兼容，所以引入了新的生命周期。



### 其他react问题

##### 1.steState是同步的还是异步的？或者2者都不准确？多个setState是怎么更新的？++

  有时是同步，又时是异步，具体要看怎么使用，如果同步的使用setState则是异步合并上去的，如果将setState放在setTimeout等异步回调里，则可以同步的拿到设置后的最新状态。

  多个setState在更新时会对其进行合并批量更新。



##### 2.虚拟dom是怎么提升性能的？++

  虚拟 dom 相当于在 js 和真实 dom 中间加了一个缓存，利用 diff 算法避免了没有必要的 dom 操作，从而提高性能。



##### 3.diff算法的理解？++

  由于找到最优解耗费的时间太长，所以采用3个策略。

  1.dom结构发生变化直接删除，重新创建，不再去比较子节点；

  2.dom结构一样的不会删除，但会更新状态

  3.同一层级的子节点，他们要通过key来区分。



##### 4.高阶组件的理解吗？++

  高阶组件是一个以组件为参数并返回一个新组件的函数。最常见的就是 Redux 的 `connect` 函数。



##### 5.Redux的流程，配合react怎么使用？++

  要点：单向数据流

  使用：先将createStore从redux中引出来创建store，然后将Provider和connect从react-redux中引出，用Provider包着根组件，并将store传入，需要访问store的子组件，通过connect将store合并到子组件的props上，子组件就可以通过props获得store的状态。子组件可以通过dispatch一个action对象，然后reducer函数会通过action对象的type属性，去触发对应的函数，从而返回新的state来更改状态。



##### 6.react版本/相较与15，升级了什么？++

  我们用的是16.8  现在最新版本是16.13

  新的diff算法，新的生命周期，hooks，feber架构，错误边界捕获，lazy



##### 7.子组件怎向父组件传值+

1. 父组件通过props来传递事件的引用，并通过回调的方式来实现。
2. 还可以通过context, context可以跨级从父组件向子组件传值，也可以子组件来获取和设置父组件暴露出来的属性值。



##### 8.知道hooks吗？为什么会出现hooks？++

​	第一问，把hooks的用法，及注意点答出来就可以了。

1. 使函数式组件也有自己的内部状态
2. 代码量更少
3. 更容易拆分



##### 9.受控组件和非受控组件的区别+

  受控组件状态由父组件维护，非受控组件状态由自身维护。受控组件设置value,非受控组件不设置value。



##### 10.react、vue相较与jquery的优势+

1. react/vue组件化开发，容易复用
2. 维护的优势
3. 虚拟dom的实现



##### 11.render和update哪个先执行?

```javascript
componentWillUpdate() //在render之前执行
componentDidUpdate()  //在render之后执行
```



##### 12.和视图没有关系的变量应该写在哪里？

​	直接用this挂在实例上



##### 13.setState除了传对象还可以传什么？

​	还可以传函数，函数返回一个对象，可以读取到上一次设置的最新状态。



##### 14.react写的循环是返回一些JSX，为什么会在组件中写一个key？

​	为了性能优化考虑，相同key的组件作比较，不然的话删除中间组件，后边的组件都要重新删除渲染。



##### 15.操作state中的数组时，用push还是concat?

​	用concat，react中大多数情况是copy出一个值。而不是在原来的值上面进行修改。



##### 16.使用过的redux中间件

​	thunk 解决异步问题



##### 17.按需加载/分包

​	babel-plugin-import



##### 18.介绍react优化 

​	减少组件的render shouldComponentUpdata()



##### 19.介绍Immuable（不可变数据对象）

  immer.js



##### 20.高阶使用

​	context 上下文  解决数据深层次传递问题

​	portal 用来解决由于父元素体积等限制问题，子元素不在父元素内渲染，但与父元素有事件交互

​	refs  用来获取组件实例

​	suspense 为了解决异步加载组件，组件没加载期间，将页面渲染成其他load组件



## react-router问题

##### 1.react-router里的`<Link>` 标签和`<a>` 标签有什么区别

​	Link灵活，会自动适配不同的历史模式，无url模式，hash模式，html5模式

​		不同模式渲染出来的a标签的href属性不一样

​	Link的to属性可以接受对象

 

##### 2.`<a>` 标签默认事件禁掉以后做什么才能实现跳转

​	history.pushState() 浏览器框发生改变，框架内部进行跳转



##### 3.react-router怎么使用

```html
 <Router history={history} createElement={createElement}>
   <Route path="/" component={App}>
     <Link />
     <Route path="*" component={NotFound} />
   </Route>
 </Router>
```



##### 4.react-router的原理+