## events

最重要模块，因为Node.js本身架构是事件式的

#### 1- 事件发射器

events对象只提供了一个对象：events.EventEmitter

EventEmitter的核心是**事件发射**和**事件监听器**功能的封装

对于每个事件，EventEmitter支持若干个事件监听器

当事件发射时，注册到这个事件的事件监听器被依次调用，事件参数作为回调函数参数传递

```javascript
var events = require('events')

var emitter = new events.EventEmitter()

emitter.on('someEvent', (ag1, ag2)=> {
    console.log('listerner1', ag1, ag2);
})

emitter.on('someEvent', (ag1, ag2)=> {
    console.log('listerner2', ag1, ag2);
})

emitter.emit('someEvent', 'byvoid', 1991)

// listerner1 byvoid 1991
// listerner2 byvoid 1991
```

api	

```javascript
// 未指定事件注册监听器
EventEmitter.on('eventName', listener)
// 发射eventName事件，传递若干可选参数到事件监听器的参数表
EventEmitter.emit('eventName', [arg1], [arg2], [...])
// 为指定事件注册一个单次监听器
EventEmitter.once('eventName', listener)  
// 移除指定事件的某个监听器, 监听器最多触发一次，触发后立即解除该监听器
EventEmitter.removeListener(event, listener)
// 移除所有事件的所有监听器， 如果指定event, 则移除指定事件的所有监听器
EventEmitter.removeListeners([events])
```

#### 2- error事件

EventEmitter定义了一个特殊的事件error, 它包含了“错误”的含义，我们遇到异常时通常会发射error事件

当error被发射时，EventEmitter规定如果没有相应的监听器，nodejs会吧它当做异常，退出程序并打印调用栈

解决方案： 为发射error事件的对象设置监听器，避免遇到错误后整个程序崩溃

也就是触发的事件，一定要是注册过监听器的，不然会报错

#### 3- 继承EventEmitter

fs,net,http在内的只要是支持事件响应的核心模块都是EventEmitter的子类



