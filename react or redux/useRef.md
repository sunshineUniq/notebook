useRef： 用来获取组件实例对象或者是DOM对象。

基本用法

```javascript
import React, { useState, useRef, useMemo, useEffect } from "react";

export default function Count() {
  const [count, setCount] = useState(0);
  const couterRef = useRef()
  const doubleCount = useMemo(() => {
    return 2 * count
  }, [count])

  useEffect(() => {
    document.title = `this value is ${count}`
    console.log(couterRef.current);
  }, [count])
  return (
    <>
    <button ref={couterRef} onClick={() => {setCount(count + 1)}}>Count: {count}, double: {doubleCount}</button>
    </>
  );
}

```

高级用法： 用来保存数据，跨周期渲染

需求：跨渲染周期保存数据

在一个组件中有什么东西可以跨渲染周期，也就是在组件被多次渲染之后依旧不变的属性？第一个想到的应该是`state`。没错，一个组件的`state`可以在多次渲染之后依旧不变。**但是，`state`的问题在于一旦修改了它就会造成组件的重新渲染**。

那么这个时候就可以使用`useRef`来跨越渲染周期存储数据，而且对它修改也不会引起组件渲染。

```javascript
import React, { useState, useRef, useMemo, useEffect } from "react";

export default function Count() {
  const [count, setCount] = useState(0);
  const couterRef = useRef(null)
  const timerId = useRef()
  const doubleCount = useMemo(() => {
    return 2 * count
  }, [count])



  useEffect(()=> {
    timerId.current = setInterval(()=> {
      setCount(count => count + 1)
    }, 1000)
  }, [])

  useEffect(()=> {
    if(count > 10) {
      clearInterval(timerId.current)
    }
  })

  useEffect(() => {
    document.title = `this value is ${count}`
    console.log(couterRef.current);
  }, [count])

  return (
    <>
    <button ref={couterRef} onClick={() => {setCount(count + 1)}}>Count: {count}, double: {doubleCount}</button>
    </>
  );
}
```

在上面的例子中，我用ref对象的current属性来存储定时器的ID，这样便可以在多次渲染之后依旧保存定时器ID，从而能正常清除定时器。

useRef 在hooks中的作用： 类似于this, 用来存放全局变量

#### createRef 和 useRef的区别

与createRef的区别，createRef每次渲染都会返回一个新的引用，而useRef每次返回相同的引用

```javascript
import React, { createRef, useRef, useState } from 'react'

export default function CompareRef() {
    const [renderIndex, setRenderIndex] = useState(1)
   const refFromUseRef = useRef()
   const refFromCreateRef = createRef()
   if(!refFromUseRef.current){
       refFromUseRef.current = renderIndex
   }
   if(!refFromCreateRef.current){
    refFromCreateRef.current = renderIndex
}
        function handleAlertClik() {
        setTimeout(()=> {
            alert(renderIndex)
        }, 3000)
    }
    return (
        <div>
            <p>current render index: {renderIndex}</p>
            <p>refFromUseRef: value : {refFromUseRef.current}</p>
            <p>refFromCreateRef: value : {refFromCreateRef.current}</p>
            <button onClick={()=> setRenderIndex(prev => prev + 1)}>cause re-render</button>
            <button onClick={handleAlertClik}>show alert</button>
        </div>
    )
}

```

useRef： 在render一次过后refFromUseRef.current就被赋值为了1

createRef: 不管render多少次，refFromCreateRef.current初始值始终都是null

就算组件重新渲染, 由于 refFromUseRef 的值一直存在(类似于 this ) , 无法重新赋值. 运行结果如下:

![](..\img\v2-9257893639285ba331a797232c848e4d_b.gif)

在renderIndex是6的时候点击show alert按钮，在renderIndex变成10的瞬间弹窗6

**为什么不是界面上 count 的实时状态?**

当我们更新状态的时候,**React 会重新渲染组件, 每一次渲染都会拿到独立的 renderIndex状态, 并重新渲染一个 handleAlertClick 函数. 每一个 handleAlertClick 里面都有它自己的 renderIndex.**

**如何让点击的时候弹出实时的 count ?**

```javascript
import React, {useState, useRef, useEffect} from 'react'

export default function CompareRef() {
    const [count, setCount] = useState(0)
    const lastestCountRef = useRef(count)
    useEffect(() => {
        lastestCountRef.current = count
    }, [count])
    
    function handleAlertClick() {
        setTimeout(()=> {
            alert('最新的count'+lastestCountRef.current)
        }, 3000)
    }
    return (
        <div>
            <p>you clicked {count}</p>
            <button onClick={() => setCount(count + 1)}>click me </button>
            <button onClick={handleAlertClick}>show alert</button>
        </div>
    )
}
```

<img src="..\img\useRef的设计原因.jpg" style="zoom:50%;" />

因为 useRef 每次都会返回同一个引用, 所以在 useEffect 中修改的时候 ,在 alert 中也会同时被修改. 这样子, 点击的时候就可以弹出实时的 count 了.

上面的问题解决了, 我们继续, 我们希望在界面上显示出上一个 count 的值.

```javascript
import React, {useState, useEffect, useRef} from 'react'

export default function PrevCount() {
    const [count, setCount] = useState(0)
    const preCount = useRef(count)
    useEffect(()=> {
        preCount.current = count
    })

    return (
        <div>
             <p>previous count: {preCount.current}</p>
             <p>you clicked {count} times</p>
            <button onClick={() => setCount(count + 1)}>click me </button>
        </div>
    )
}

```

![image-20210311133749486](../img\image-20210311133749486.png)