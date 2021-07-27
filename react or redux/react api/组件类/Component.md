#####  1- Component

`react`对`Component`做了些什么。

```react
react/src/ReactBaseClasses.js
function Component(props, context, updater) {
  this.props = props;
  this.context = context;
  this.refs = emptyObject;
  this.updater = updater || ReactNoopUpdateQueue;
}
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

contrustClassInstance

```react
react-reconciler/src/ReactFiberClassComponent.js
```

**我们声明的类组件是什么时候以何种形式被实例化的呢？**

这就是`Component`函数，其中`updater`对象上保存着更新组件的方法。