useRef

利用useRef获取需要监听的元素

一般是监听列表外层的父盒子，注册scroll监听，当发现滚动内容的高度-滚动的高度- 盒子的可视高度 < 临界距离时，

这个时候判断是否有下一页，是否正在请求下一页，如果有下一页且没有正在请求，就可以请求下一页了

注意; pageNo 和totalPage 的存放问题

函数组件利用好useRef进行全局的存储

如果有tab切换需要清除ref内存储的变量

```javascript
  useEffect(() => {
    if (activeTabIndex === 1 && listRef.current && listWrapRef.current) {
      // 监听list的滚动事件
      listWrapRef.current.addEventListener('scroll', () => {
        if (listWrapRef.current.scrollHeight - listWrapRef.current.scrollTop - listWrapRef.current.clientHeight < 100) {
          // 请求下一页
          if (pageInfoRef.current.pageNo < pageInfoRef.current.totalPage && !loading) {
            console.log('fetchs');
            const newPageNo = pageInfoRef.current.pageNo + 1
            pageInfoRef.current.pageNo = newPageNo
            getConsumptionListByPageNo(newPageNo)
          }
        }
      });
    }
  });
```

