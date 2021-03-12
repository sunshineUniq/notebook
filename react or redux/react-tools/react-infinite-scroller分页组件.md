https://www.npmjs.com/package/react-infinite-scroller

## state定义所需初始值

```javascript
   this.state = {
      hasMore: true,
      pageNum: 1,
      pageSize: 10,
      data: []
    };
```

## 加载更多

// 获取下一页信息
**不需要在 componentDidMount()获取数据设置hasMore为true时已经开始加载第一页数据了**

```javascript
  getMore = () => {
    this.$post("/community/list", {
      pageNum: this.state.pageNum,
      pageSize: this.state.pageSize
    }).then(res => {
      this.setState({
        pageNum: this.state.pageNum + 1,
        hasMore: res.data.hasNextPage,
        data: this.state.data.concat(res.data.list)//数组连接
      });
    });
  };
```

## render内容区域

```javascript
 render() {
    const data = this.state.data;
    return (
      <div style={{ height: "calc(100vh - 60px)", overflow: "auto" }}>
        <InfiniteScroll
          className="list-contents"
          pageStart={1} //首页为1，可根据自己的具体需求
          loadMore={this.getMore.bind(this)}
          loader={
            <div className="loader" key={0}>
              Loading ...
            </div>
          }
          useWindow={false}  //****将滚动侦听器添加到窗口，或者添加组件的parentNode****
          hasMore={this.state.hasMore}
        >
          {this.renderItemList(data)}  //自定义渲染内容可以在这写也可以提出来
        </InfiniteScroll>
      </div>
    );
  }
```

## Props

| Name              | Type        | Default | Description                                                  |
| :---------------- | :---------- | :------ | :----------------------------------------------------------- |
| `element`         | `Component` | `'div'` | Name of the element that the component should render as.     |
| `hasMore`         | `Boolean`   | `false` | Whether there are more items to be loaded. Event listeners are removed if `false`. |
| `initialLoad`     | `Boolean`   | `true`  | Whether the component should load the first set of items.    |
| `isReverse`       | `Boolean`   | `false` | Whether new items should be loaded when user scrolls to the top of the scrollable area. |
| `loadMore`        | `Function`  |         | A callback when more items are requested by the user. Receives a single parameter specifying the page to load e.g. `function handleLoadMore(page) { /* load more items here */ }` } |
| `loader`          | `Component` |         | A React component to render while more items are loading. The parent component must have a unique key prop. |
| `pageStart`       | `Number`    | `0`     | The number of the first page to load, With the default of `0`, the first page is `1`. |
| `getScrollParent` | `Function`  |         | Override method to return a different scroll listener if it's not the immediate parent of InfiniteScroll. |
| `threshold`       | `Number`    | `250`   | The distance in pixels before the end of the items that will trigger a call to `loadMore`. |
| `useCapture`      | `Boolean`   | `false` | Proxy to the `useCapture` option of the added event listeners. |
| `useWindow`       | `Boolean`   | `true`  | Add scroll listeners to the window, or else, the component's `parentNode`. |