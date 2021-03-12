

## react-transition-group 一个官网提供的动画过度库



安装该组件库：yarn add react-transition-group

该组件库包括四个组件：Transition（不太用了） CSSTransition（最常用） SwitchTransition TransitionGroup（列表中元素的动画）

```javascript
npm install react-transition-group --save
```

## CSSTransition

此组件是在转换的出现、进入、退出阶段应用一对类名(也就是className),靠这个来激活CSS动画。所以参数和平时的className不同，参数为：`classNames`

参数：（主要）in, timeout, unmountOnExit, classNames, 用法同Transition。看如下例子：

```javascript
import React, {useState} from 'react'
import {CSSTransition} from 'react-transition-group'
import './index.css'

export default function Star() {
    const [star, setStar] = useState(false)
    const handleStar = () => {
        setStar(!star)
    }
    return (
        <div>
            <button onClick={handleStar}>click to start</button>
            <CSSTransition
                in={star}
                timeout={300}
                classNames = 'star'
                unmountOnExit
            >
                <div className="star">⭐</div>
            </CSSTransition>
        </div>
    )
}
 
```

效果是点击button 显示星星，在点击消失星星的动画！

参数`classNames="star"`, 组件会找对应状态的className, 如下

```scss
.star {
    display: inline-block;
    margin-left: 0.5rem;
    transform: scale(1.25);
  }
  .star-enter {
    opacity: 0.01;
    transform: translateY(-100%) scale(0.75);
  }
  .star-enter-active {
    opacity: 1;
    transform: translateY(0%) scale(1.25);
    transition: all 300ms ease-out;
  }
  .star-exit {
    opacity: 1;
    transform: scale(1.25);
  }
  .star-exit-active {
    opacity: 0;
    transform: scale(4);
    transition: all 300ms ease-in;
  }
```

依次执行的顺序是

```javascript
1、星星显示 对应的class为star-enter star-enter-active 动画走完为star-enter-done
2、星星消失 对应的class为star-exit  star-exit-active 动画走完为star-exit-done
```

```
classNames={{
 appear: 'my-appear',
 appearActive: 'my-active-appear',
 enter: 'my-enter',
 enterActive: 'my-active-enter',
 enterDone: 'my-done-enter,
 exit: 'my-exit',
 exitActive: 'my-active-exit',
 exitDone: 'my-done-exit,
}}
```

每个阶段的钩子函数同Transition.