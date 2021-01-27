#### Children

含义： 提供了一堆帮你处理props.children的方法，因为children是一个类似数组但不是数组的数据结构，如果要对其进行处理可以使用React.children外挂方法

```javascript
var Children = {
  map: mapChildren,
  forEach: forEachChildren,
  count: countChildren,
  toArray: toArray,
  only: onlyChild
};
```