主要使用场景：css样式模块化 styled-components

友联：

styled-components的基本使用指南：https://www.jianshu.com/p/2d5f037c7df9

官网：https://styled-components.com/

#### 安装

```powershell
npm install --save styled-components
```

#### 基本用法

1- 声明一个带样式的h1组件

```javascript

import styled from 'styled-components'

const Title = styled.h1`
  font-size: 18px;
  text-align: center;
  color: red;
`

function App() {
  return (
    <div className="App">
      <Title>我是标题</Title>
    </div>
  );
}

export default App;
```

2- 样式组件的props

```javascript
const Button = styled.button`
  background: ${props => props.primary? 'palevioletred': 'white'};
  color: ${props => props.primary? 'white' : 'palevioletred'};
  font-size: 20px;
  margin: 10px;
  padding: 25px 10px;
  border: 2px solid palevioletred;
  border-radius: 6px;
`
function App() {
  return (
    <div className="App">
     <Button>Normal</Button>
     <Button primary>primary</Button>
    </div>
  );
}
```

3- 组件样式的重定制：基础组件的复用

```javascript
const OrangeEmptyBtn = styled(Button)`
  color: orange;
  border-color: orange;
`
render(
  <div>
    <Button>Normal Button</Button>
    <TomatoButton>Tomato Button</TomatoButton>
  </div>
);
```

4- 修改样式组件的标签名： 复用

```javascript
<Button as='a' href="/">Link With Button styles</Button>
<OrangeEmptyBtn as="div">Link with OrangeEmptyBtn styles</OrangeEmptyBtn>
```

as也可以是组件，需要有{}

```javascript
const ReverseButton = (props) => <Button {...props} children={props.children.split('').reverse()}/>
...
<OrangeEmptyBtn as={ReverseButton}>Custom Button with OrangeEmptyBtn Styles</OrangeEmptyBtn>
```

4- 使用styled(组件/标签)的方式给组件设置样式代替使用className

```javascript
const Link = ({ className, children }) => (
  <a className={className} >{children}</a>
)

const StyledLink = styled(Link)`
  font-size: 40px;
  color: red;
  text-decoration: none;
`
<Link>link</Link>
<StyledLink>styled Link</StyledLink>
```

5- styled-component能自己区分哪些prop是标签原生的属性，哪些是定制的

```javascript
// Create an Input component that'll render an <input> tag with some styles
const Input = styled.input`
  padding: 0.5em;
  margin: 0.5em;
  color: ${props => props.inputColor || "palevioletred"};
  background: papayawhip;
  border: none;
  border-radius: 3px;
`;

// Render a styled text input with the standard input color, and one with a custom input color
render(
  <div>
    <Input defaultValue="@probablyup" type="text" />
    <Input defaultValue="@geelen" type="text" inputColor="rebeccapurple" />
  </div>
);
```

Note: 在render函数外定义style-component

6- selector 

& : 指向当前组件

```javascript
const Ting = styled.div.attrs(() => ({ tabIndex: 0 }))`
  color: blue;
  &:hover{
    color: red;
  }; 
  & ~ & {
    background: tomato;
  };  // 给兄弟Ting 设置样式，不需要相邻
  & + & {
    background: red; /* 兄弟Ting 设置样式 */
  };
  &.something{
    background: orange; /* 给类名是something的Ting设置样式*/
  };
  .something-else & {
    background: yellow; /* 被类名是something-else 包裹的Ting */
  }；
  .kid{
    background: red; 
    color: white;  /* 没有&， 表示Ting的子元素*/
  }
`

```

7- 样式优先级 &&

```javascript
import styled, {createGlobalStyle} from 'styled-components'

const Text1 = styled.div`
  && {
    color: red;
  }
`
const GlobalStyle = createGlobalStyle`
  div${Text1} {
    color: blue;
  }
`

<GlobalStyle/>
<Text1>测试样式优先级</Text1>
```

8- .attrs

```javascript
const Input = styled.input.attrs(props => ({
  // we can define static props
  type: "text",

  // or we can define dynamic ones
  size: props.size || "1em",
}))`
  color: palevioletred;
  font-size: 1em;
  border: 2px solid palevioletred;
  border-radius: 3px;

  /* here we use the dynamically computed prop */
  margin: ${props => props.size};
  padding: ${props => props.size};
`;

render(
  <div>
    <Input placeholder="A small text input" />
    <br />
    <Input placeholder="A bigger text input" size="2em" />
  </div>
);
```

9- animation 

```javascript
const rotate = keyframes`
  from {
    transform: rotate(0deg)
  }
  to {
    transform: rotate(360deg)
  }
`
const Rotate = styled.div`
  animation: ${rotate} 2s linear infinite;
  padding: 2rem 1rem;
  font-size: 1.2rem;
  display: inline-block;
`
<Rotate>👋👋</Rotate>
```

写法二

```javascript
import styled, {createGlobalStyle, keyframes, css} from 'styled-components'

const rotate = keyframes`
  from {
    transform: rotate(0deg)
  }
  to {
    transform: rotate(360deg)
  }
`
const styles = css`
   animation: ${rotate} 2s linear infinite;
`
const Rotate = styled.div`
  ${styles}
  padding: 2rem 1rem;
  font-size: 1.2rem;
  display: inline-block;
`
```

10- react-native

```javascript
import styled from 'styled-components/native'

const StyledView = styled.View`
  background-color: papayawhip;
`

const StyledText = styled.Text`
  color: palevioletred;
`
```

11- style object

```javascript
// Static object
const Box = styled.div({
  background: 'palevioletred',
  height: '50px',
  width: '50px'
});

// Adapting based on props
const PropsBox = styled.div(props => ({
  background: props.background,
  height: '50px',
  width: '50px'
}));
```

