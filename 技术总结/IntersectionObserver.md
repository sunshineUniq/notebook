`**IntersectionObserver**`**接口** (从属于[Intersection Observer API](https://developer.mozilla.org/en-US/docs/Web/API/Intersection_Observer_API)) 提供了一种异步观察目标元素与其祖先元素或顶级文档视窗([viewport](https://developer.mozilla.org/zh-CN/docs/Glossary/Viewport))交叉状态的方法。祖先元素与视窗([viewport](https://developer.mozilla.org/zh-CN/docs/Glossary/Viewport))被称为**根(root)。**

当一个`IntersectionObserver`对象被创建时，其被配置为监听根中一段给定比例的可见区域。

一旦IntersectionObserver被创建，则无法更改其配置，所以一个给定的观察者对象只能用来监听可见区域的特定变化值；然而，你可以在同一个观察者对象中配置监听多个目标元素。

| 属性和方法             | 解释                                                         |
| ---------------------- | ------------------------------------------------------------ |
| IntersectionObserver() | 创建一个新的`IntersectionObserver`对象，当其监听到目标元素的可见部分穿过了一个或多个**阈(thresholds)**时，会执行指定的回调函数。 |
| root                   | 所监听对象的具体祖先元素, 如果未传入值或值为`null`，则默认使用顶级文档的视窗。 |
| rootMargin             | 计算交叉时添加到**根(root)**边界盒[bounding box](https://developer.mozilla.org/en-US/docs/Glossary/bounding_box)的矩形偏移量， 可以有效的缩小或扩大根的判定范围从而满足计算需要。此属性返回的值可能与调用构造函数时指定的值不同，因此可能需要更改该值，以匹配内部要求。所有的偏移量均可用**像素(pixel)**(`px`)或**百分比(percentage)**(`%`)来表达, 默认值为"0px 0px 0px 0px"。 |
| thresholds             | 一个包含阈值的列表, 按升序排列, 列表中的每个阈值都是监听对象的交叉区域与边界区域的比率。当监听对象的任何阈值被越过时，都会生成一个通知(Notification)。如果构造器未传入值, 则默认值为0。 |
| disconnect()           | 使`IntersectionObserver`对象停止监听工作。                   |
| observe()              | 使`IntersectionObserver`开始监听一个目标元素。               |
| takeRecords()          | 返回所有观察目标的[`IntersectionObserverEntry`](https://developer.mozilla.org/zh-CN/docs/Web/API/IntersectionObserverEntry)对象数组。 |
| unobserve()            | 使`IntersectionObserver`停止监听特定目标元素。               |

 实例：

```javascript
var intersectionObserver = new IntersectionObserver(function(entries) {
  // If intersectionRatio is 0, the target is out of view
  // and we do not need to do anything.
  if (entries[0].intersectionRatio <= 0) return;

  loadItems(10);
  console.log('Loaded new items');
});
// start observing
intersectionObserver.observe(document.querySelector('.scrollerFooter'));
```

