什么是虚拟DOM？

Js对象，描述真实DOM

Diff 算法比较的是什么？

新旧虚拟DOM

diff 算法的复杂度？

O（N），比较两个树的算法复杂度是O（N^3), React通过两个假设降低了算法复杂度

React降低比较两棵虚拟DOM树算法复杂度的假设是？

1） 两个元素种类不同，生成两个不同的树

2） 利 Key属性，判断key标识的元素是否发生变化



diff 算法

1- 当根节点是不同类型时

不比较子节点，直接拆除重建，涉及的周期函数

componentWillUnmount

componentWillMount

componentDidMount

2- 当根节点是相同的DOM元素类型时

只比较根节点的属性，只更新变化的属性

3- 当根节点是相同的组件类型时

不销毁组件实例，只比较根节点的属性变化进行更新操作

componentWillReceiveProps

componentWillUpdate

react无法直接知道如何更新真实DOM树，需要在组件更新并且执行render方法后，根据render返回的虚拟DOM结构决定如何更新真实DOM树