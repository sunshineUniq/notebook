### 组件类

组件类API

- Component

- PureComponent

- memo 高阶组件

- forwardRef 高阶组件

- lazy

- Suspense

- Fragment

- Profiler

- StrictMode

  

##### 1- Component

`react`对`Component`做了些什么。

```react/src/ReactBaseClasses.js```

```react
function Component(props, context, updater) {
  this.props = props;
  this.context = context;
  this.refs = emptyObject;
  this.updater = updater || ReactNoopUpdateQueue;
}
```

这就是`Component`函数，其中`updater`对象上保存着更新组件的方法。

**我们声明的类组件是什么时候以何种形式被实例化的呢？**

```react-reconciler/src/ReactFiberClassComponent.js```

contrustClassInstance

```react
function constructClassInstance(
	workInProgress,
  ctor,
  props
) {
	const instance = new ctor(props, context)
  instance.updater = {
    isMounted,
    enqueueSetState() {
      /* setState触发这里面的逻辑 */
    }，
    enqueueReplaceState() {},
    enqueueForceUpdate(){
      /* forceUpdate 触发这里的逻辑 */
    }
  }
}
```

对于Component, react 处理逻辑还是很简单的， 实例化我们类组件，然后赋值updater 对象， 负责组件的更新。然后在组件的各个阶段，执行类函数的render函数和对应的生命周期函数

##### 2- PureComponent

`PureComponent`和 `Component`用法，差不多一样，唯一不同的是，纯组件`PureComponent`会浅比较，`props`和`state`是否相同，来决定是否重新渲染组件。所以一般用于**性能调优**，减少**render**次数。

```react
class Index extends React.PureComponent{
    constructor(props){
        super(props)
        this.state={
           data:{
              name:'alien',
              age:28
           }
        }
    }
    handerClick= () =>{
        const { data } = this.state
        data.age++
        this.setState({ data })
    }
    render(){
        const { data } = this.state
        return <div className="box" >
        <div className="show" >
            <div> 你的姓名是: { data.name } </div>
            <div> 年龄： { data.age  }</div>
            <button onClick={ this.handerClick } >age++</button>
        </div>
    </div>
    }
}
```

**点击按钮，没有任何反应**，因为`PureComponent`会比较两次`data`对象，都指向同一个`data`,没有发生改变，所以不更新视图。

解决这个问题很简单，只需要在`handerClick`事件中这么写：

```react
 this.setState({ data:{...data} })
```

**浅拷贝**就能根本解决问题。

##### 3- memo

React.memo和PureComponent 的区别和共同点

共同点： 都可以用作性能优化

不同点：1- React.memo 使用范围更广，高阶组件、函数组件、类组件都能使用， PureComponent 只能类组件继承

​				2- React.memo只对props进行浅比较决定是否渲染， PureComponent针对props 和State

React.memo接受两个参数，第一个参数原始组件本身，第二个参数，可以根据一次更新中`props`是否相同决定原始组件是否重新渲染。是一个返回布尔值，`true` 证明组件无须重新渲染，`false`证明组件需要重新渲染，这个和类组件中的`shouldComponentUpdate()`正好相反 。

**React.memo: 第二个参数 返回 `true` 组件不渲染 ， 返回 `false` 组件重新渲染。**

**shouldComponentUpdate: 返回 `true` 组件渲染 ， 返回 `false` 组件不渲染。**

