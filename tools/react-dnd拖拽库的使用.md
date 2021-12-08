功能：实现拖拽

基本概念

- backend： 抹平浏览器差异， 关注dom 事件
- item: 拖放发生时，用一个数据对象描述当前的元素
- type: 类似redux的actions type
- Monitor: 存储拖拽的状态并提供查询
- Connector: 连接组件和backend, 可以让backend获取到dom 
- dragSource: 将组件使用 `DragSource` 包裹让它变得可以拖动，`DragSource` 是一个高阶组件：

```react
DragSource(type, spec, collect)(Component)
// type
只有DragSource注册的类型和DragTarget注册的类型完全匹配时才可以drop
// spec: 描述DragSource如何对拖放事件作出反应
-	beginDrag(props, monitor, component)
- endDrag(props, monitor, component)
- canDrag(props, monitor)
- isDragging(props, monitor)
// collect: 类似于redux connector 里面的mapStateToProps
- 每个函数都会接收到connect和monitor两个参数
- connect 用来和DnD后端联系
- monitor用来查询拖拽状态信息
```

- DropTarget: 将组件使用 `DropTarget` 包裹让它变得可以响应 drop，`DropTarget` 是一个高阶组件：

```react
DropTarget(type, spec, collect)(Component)
// spec: 描述DropTarget如何对拖放事件作出反应
- drop(props, monitor, component)返回值可以让DragSource在endDrag事件内通过monitor获取
- hover(props, monitor, component)
- canDrop(props, monitor)
```

- DragDropContext: 包裹根组件， 可以定义backend, DropTarget 和 DropTarget包装过的组件必须在DragDropContext包裹的组件中

```react
DragDropContext(backend)(RootComponent)
```

