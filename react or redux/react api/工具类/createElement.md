```react
React.createElement(
  type,
  [props],
  [...children]
)
```

`createElement`参数：

**第一个参数:**如果是组件类型，会传入组件，如果是`dom`元素类型，传入`div`或者`span`之类的字符串。

**第二个参数:**:第二个参数为一个对象，在`dom`类型中为**属性**，在`组件`类型中为**props**。

**其他参数:**，依次为`children`，根据顺序排列。

**createElement做了些什么？**

经过`createElement`处理，最终会形成 `$$typeof = Symbol(react.element)`对象。对象上保存了该`react.element`的信息。

