1- Jsx转化成js

- babel工具 React.createElement()
  - 如何区分组件和dom 节点： 首字母是否大写--大写：变量  小写：字符串

```react
function createElement(type, config, children) {
  return ReactElement(
  	// 见下面
  )
}
```



2- ReactElement

```react
ReactElement只是一个用来承载信息的容器，他会告诉后续的操作这个节点的以下信息：

type类型，用于判断如何创建节点
key和ref这些特殊信息
props新的属性内容
$$typeof用于确定是否属于ReactElement
const ReactElement = function(type, key, ref, self, source, owner, props){
  const element = {
    $$typeof: REACT_ELEMENT_TYPE,
    type: tyope
    key: key
    ref: ref
    _owner: owner
  }
  return element
}
```



3- Component

```react
function Component(props, context, updater) {
  // 将入参挂在到this上
  this.props = props;
  this.context = context;
  this.ref = emptyObject;
  this.updater = updater || ReactNoopUpdateQueue;
}
Component.prototype.isReactCompoent = {};
Component.prototype.setState = function(partialState, callback) {
  	// ....
		this.upater.enqueueSetState(this, partialState, callback, 'setState')
}
Component.prototype.forceUpdate = function(callback){
  	this.updater.enqueueForceUpdate(this, callback, 'forceUpdate')
}

function PureComponent(props, context, updater) {
  // 同component
}
// 使用es5的混合式继承修改PureComponent的原型
// 增加标识
PureComponentPrototype.isPureReactComponent = true
```



4- createRef & ref

```typescript
ref的使用方式
-	字符串 （组件或元素挂载之后会将元素或组件实例赋值给字符串变量， 函数组件没有实例，所以会报错）
- 函数 
- createRef api {current: null}
function createRef(): RefObject{
  const refObject = {
    current: null
  }
  return refObject
}
```



5- forwardRef

```typescript
function forwardRef<Props, ElementType: React$ElementType>(render: (props: Props, ref: React$Ref<ElementType>)   		=> React$Mode) {
  return {
    $$typeof: REACT_FORWARD_REF_TYPE,
   	render
  }
}
```



6- context

>两种实现方式
>
>childContextType
>
>createContext

```react
function createContext<T>(defaultValue: T) {
  const context = {
    $$typeof: REACT_CONTEXT_TYPE,
    _currentValue = defaultValue,
    _currentValue2 = defaultValue,
    Provider: (null: any),
    Consumer: (null: any)
  }
  context.Provider = {
		$$typeof: REACT_PROVIDER_TYPE,
    _context: context,
	}
	context.Consumer = context
	return context
}
```



7- ConcurrentMode

被ConcurrentMode包裹的组件优先级会比较高，结合flushSync使用

```
  React.ConcurrentMode = REACT_CONCURRENT_MODE_TYPE;
```



8- Suspense

- 组件内部有异步操作，在promise.resolve前展示fallback 的内容， resolve后展示组件
- 通常结合lazy使用
- 特效： 包裹的组件只要有一个pending就展示fallback的内容

```
  Suspense: REACT_SUSPENSE_TYPE
```

```react
function lazy<T, R>(ctor: () => Thenable<T, R>): LazyComponent<T> {
  return {
    $$typeof: REACT_LAZY_TYPE,
    _ctor: ctor,
    // React uses these fields to store the result.
    _status: -1,
    _result: null,
  };
}
```



9- hooks

```react
export function useState<S>(initialState: (() => S) | S) {
  const dispatcher = resolveDispatcher();
  return dispatcher.useState(initialState);
}

function resolveDispatcher() {
  const dispatcher = ReactCurrentOwner.currentDispatcher;
  return dispatcher;
}

const ReactCurrentOwner = {
  current: (null: null | Fiber),
  currentDispatcher: (null: null | Dispatcher),
};

```



10- Children

>`React.Children.map`的一个特性了，那就是对每个节点的`map`返回的如果是数组，那么还会继续展开，这是一个递归的过程。

![](imgs/react-children-map.png)



11- others

memo 

Fragment 

StrictMode

cloneElement

createFactory
