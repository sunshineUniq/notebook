1-  useEffect是不能直接用 async await 语法糖的。

```react

/* 错误用法 ，effect不支持直接 async await 装饰的 */
 useEffect(async ()=>{
        /* 请求数据 */
      const res = await getUserInfo(payload)
 },[ a ,number ])
```

 如果想使用async await需要对effect进行一层包装

```react
const asyncEffect = (callback, deps) => {
  useEffect(() => {
    callback()
  }, deps)
}
```

2- useEffect和useLayoutEffect的区别和各自的使用注意事项

useEffect执行顺序： 组件更新挂载完成 ---> 浏览器dom 绘制完成 ---->执行useEffect回调

useLayoutEffect执行顺序：组件更新挂载完成 ---> 执行useLayoutEffect回调 ---->浏览器dom 绘制完成

注意事项：

useEffect中重新请求数据，渲染视图过程中，肯定会造成页面闪动

useLayoutEffect 回调函数的代码可能会阻塞浏览器的绘制， 引起页面卡顿

具体使用哪个需要看实际场景

```react

const DemoUseLayoutEffect = () => {
    const target = useRef()
    useLayoutEffect(() => {
        /*我们需要在dom绘制之前，移动dom到制定位置*/
        const { x ,y } = getPositon() /* 获取要移动的 x,y坐标 */
        animate(target.current,{ x,y })
    }, []);
    return (
        <div >
            <span ref={ target } className="animate"></span>
        </div>
    )
}
```

3- useMemo的使用

- useMemo可以减少不必要的循环，减少不必要的渲染。

  ```react
  
  /* 用 useMemo包裹的list可以限定当且仅当list改变的时候才更新此list，这样就可以避免selectList重新循环 */
   {useMemo(() => (
        <div>{
            selectList.map((i, v) => (
                <span
                    className={style.listSpan}
                    key={v} >
                    {i.patentName} 
                </span>
            ))}
        </div>
  ), [selectList])}
  ```

- useMemo可以减少子组件的渲染次数

  ```react
   useMemo(() => (
      <Modal
          width={'70%'}
          visible={listshow}
          footer={[
              <Button key="back" >取消</Button>,
              <Button
                  key="submit"
                  type="primary"
               >
                  确定
              </Button>
          ]}
      > 
       { /* 减少了PatentTable组件的渲染 */ }
          <PatentTable
              getList={getList}
              selectList={selectList}
              cacheSelectList={cacheSelectList}
              setCacheSelectList={setCacheSelectList} />
      </Modal>
   ), [listshow, cacheSelectList])
  ```

  

- **useMemo让函数在某个依赖项改变的时候才运行，这可以避免很多不必要的开销。**

  ```react
  
  const DemoUseMemo=()=>{
    /* 用useMemo 包裹之后的log函数可以避免了每次组件更新再重新声明 ，可以限制上下文的执行 */
      const newLog = useMemo(()=>{
          const log =()=>{
              console.log(6666)
          }
          return log
      },[])
      return <div onClick={()=>newLog()} ></div>
  }
  ```

  **这里要注意⚠️⚠️⚠️的是如果被useMemo包裹起来的上下文,形成一个独立的闭包，会缓存之前的state值,如果没有加相关的更新条件，是获取不到更新之后的state的值的，如下边👇⬇️**

   ```react
  
  const DemoUseMemo=()=>{
      const [ number ,setNumber ] = useState(0)
      const newLog = useMemo(()=>{
          const log =()=>{
              /* 点击span之后 打印出来的number 不是实时更新的number值 */
              console.log(number)
          }
          return log
        /* [] 没有 number */  
      },[])
      return <div>
          <div onClick={()=>newLog()} >打印</div>
          <span onClick={ ()=> setNumber( number + 1 )  } >增加</span>
      </div>
  }
   ```

  

3- useMemo和useCallback的区别

useMemo返回的是函数运行的结果

useCallback返回的是函数

> 父组件传递一个函数给子组件的时候，由于是无状态组件每一次都会重新生成新的props函数，这样就使得每一次传递给子组件的函数都发生了变化，这时候就会触发子组件的更新，这些更新是没有必要的，此时我们就可以通过usecallback来处理此函数，然后作为props传递给子组件。

**这里应该提醒的是，useCallback ，必须配合 react.memo pureComponent ，否则不但不会提升性能，还有可能降低性能。**

```react
/* 用react.memo */
const DemoChildren = React.memo((props)=>{
   /* 只有初始化的时候打印了 子组件更新 */
    console.log('子组件更新')
   useEffect(()=>{
       props.getInfo('子组件')
   },[])
   return <div>子组件</div>
})


const DemoUseCallback=({ id })=>{
    const [number, setNumber] = useState(1)
    /* 此时usecallback的第一参数 (sonName)=>{ console.log(sonName) }
     经过处理赋值给 getInfo */
    const getInfo  = useCallback((sonName)=>{
          console.log(sonName)
    },[id])
    return <div>
        {/* 点击按钮触发父组件更新 ，但是子组件没有更新 */}
        <button onClick={ ()=>setNumber(number+1) } >增加</button>
        <DemoChildren getInfo={getInfo} />
    </div>
}
```

