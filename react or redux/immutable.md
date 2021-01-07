# 一、作用

immutable对象是不可直接赋值的对象，它可以有效的避免错误赋值的问题

# 二、immutable在react中的使用

安装

```undefined
npm install immutable
```

使用

```javascript
const { Map } = require('immutable');
const map1 = Map({ a: 1, b: 2, c: 3 });
const map2 = map1.set('b', 50);
map1.get('b') + " vs. " + map2.get('b'); // 2 vs. 50
```



在react中，immutable主要是防止state对象被错误赋值。

- 将js对象转成immutable对象

```js
import { fromJS } from 'immutable';
const defaultState = fromJS({
  todoList: []
});
```

- 获取属性

```csharp
state.get('todoList'); // 获取store中的todoList
state.get(['Main', 'todoList']); // 获取Main组件中store的todoList
```

- 改变属性

```csharp
state.set('todoList', action.value);  // 设置单个属性值
// 设置多个属性
state.merge({
  todoList: fromJS(action.value), // 由于action.value是js对象所以要转成immutable对象
});
```

- 将immutable对象转成js对象

```csharp
state.get('todoList').toJS(); // 把todoList转成js数组
```