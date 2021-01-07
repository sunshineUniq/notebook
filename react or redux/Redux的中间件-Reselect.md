```javascript
import { createSelector } from 'reselect'

const shopItemsSelector = state => state.shop.items
const taxPercentSelector = state => state.shop.taxPercent

const subtotalSelector = createSelector(
  shopItemsSelector,
  items => items.reduce((acc, item) => acc + item.value, 0)
)

const taxSelector = createSelector(
  subtotalSelector,
  taxPercentSelector,
  (subtotal, taxPercent) => subtotal * (taxPercent / 100)
)

export const totalSelector = createSelector(
  subtotalSelector,
  taxSelector,
  (subtotal, tax) => ({ total: subtotal + tax })
)

let exampleState = {
  shop: {
    taxPercent: 8,
    items: [
      { name: 'apple', value: 1.20 },
      { name: 'orange', value: 0.95 },
    ]
  }
}

console.log(subtotalSelector(exampleState)) // 2.15
console.log(taxSelector(exampleState))      // 0.172
console.log(totalSelector(exampleState))    // { total: 2.322 }
```



## 安装

 ```javascript
npm install reselect
 ```

### 用途

减少重复计算

**Reselect这个中间件要解决的问题是:`在组件交互操作的时候,state发生变化的时候如何减少渲染的压力.在Reselect中间中使用了缓存机制**

## 特点

- Selector可以计算衍生的数据,可以让Redux做到存储尽可能少的state。
- Selector比较高效,只有在某个参数发生变化的时候才发生计算过程.
- Selector是可以组合的,他们可以作为输入,传递到其他的selector.





