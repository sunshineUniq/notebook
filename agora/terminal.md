Custom-terminal

- 根据选中的container建立connect

- 新增的terminal默认建立同样的连接
- 关闭terminal 需要关闭当前bash 
- 需要区分系统展示bash或cmd文案，支持修改
- 切换container, 原先的terminals需要全部关闭

管理状态

​	terminals

​	currentTerminal

​	currentContainer 这个在context里面，需要看下怎么监听这个值的变化

​		- 监听context的containerId值的变化， setState 传入子组件 ide-terminal



terminal 的功能

​	初始化时有container建立连接

​	切换tab时不需要考虑连接的问题



rename

-  input 校验
  - 非空校验：A name must be provided
  - 全部删除，提示，enter 或失去焦点不修改名字



electron

- 没有containerId
- 
