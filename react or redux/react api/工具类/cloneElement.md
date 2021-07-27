##### 1- createElement和cloneElement的区别

`createElement`把我们写的`jsx`，变成`element`对象

`cloneElement`的作用是以 `element` 元素为样板克隆并返回新的 `React` 元素， 返回元素的 `props` 是将新的 `props` 与原始元素的 `props` 浅层合并后的结果。

##### 2- cloneElement的应用

**一些开源项目，或者是公共插槽组件中**， 在组件中，劫持`children element`，然后通过`cloneElement`克隆`element`，混入`props`。

经典的案例就是 `react-router`中的`Swtich`组件，通过这种方式，来匹配唯一的 `Route`并加以渲染

我们设置一个场景，在组件中，去劫持`children`，然后给`children`赋能一些额外的`props`:

```react
function FatherElement({children}) {
  const newChildren = React.cloneElement(children, {age: 18})
  return <div>{newChildren}</div>
}

function SonComponent(props) {
  console.log(props) 
  return <div>hello, world</div>
}

class Index extends React.Component{
  render() {
    return <div className="box">
    	<FatherComponent>
      	<SonComponent name="alien"/>
      </FatherComponent>
    </div>
  }
}

// {name: alien, age: 18}
```



