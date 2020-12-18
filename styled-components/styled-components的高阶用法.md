## 高阶用法-- 插件

### 1- 服务端渲染插件 ```babel-plugin-styled-components```

```js
npm install --save-dev babel-plugin-styled-components
```

- displayName: 支持配置是否在React DevTools中展示你命名的样式组件

```javascript
{
  "plugins": [
    [
      "babel-plugin-styled-components",
      {
        "displayName": false // 不展示样式组件的名字
      }
    ]
  ]
}
```

- fileName: 默认displayName带fileName， 支持配置是否带fileName

```javascript
{
  "plugins": [
    [
      "babel-plugin-styled-components",
      {
        "fileName": false
      }
    ]
  ]
}
```

使用场景：组件测试

- 该插件自带压缩功能，可以通过配置取消

  此插件执行两种类型的缩小：一种是从CSS中删除所有空白和注释，另一种是transiles标记的模板文本，将有价值的字节保留在bundle之外。

```javascript
{
  "plugins": [
    ["babel-plugin-styled-components", {
      "minify": false,
      "transpileTemplateLiterals": false
    }]
  ]
}
```

- Dead code Elimination (消除无用代码)

  将无用代码标记成pure annotation

```javascript
{
  "plugins": [
    ["babel-plugin-styled-components", {
      "pure": true
    }]
  ]
}
```

原理：使用babel helper标记样式组件和类库，使用 #__PURE__ js注释

- Template String Transpilation

```javascript
{
  "plugins": [
    [
      "babel-plugin-styled-components",
      {
        "transpileTemplateLiterals": false
      }
    ]
  ]
}
```

当开启时效果如下：

开启前

```javascript
var _templateObject = _taggedTemplateLiteral(['width: 100%;'], ['width: 100%;'])
function _taggedTemplateLiteral(strings, raw) {
  return Object.freeze(Object.defineProperties(strings, { raw: { value: Object.freeze(raw) } }))
}
var Simple = _styledComponents2.default.div(_templateObject)
```

开启后

```javascript
var Simple = _styledComponents2.default.div(['width: 100%;'])
```

- Namespace

```javascript
{
  "plugins": [
    ["babel-plugin-styled-components", {
      "namespace": "my-app"
    }]
  ]
}
```

使用命名空间后的代码

```javascript
_styledComponents2.default.div.withConfig({
  displayName: 'code__before',
  componentId: 'my-app__sc-3rfj0a-1',
})(['color:blue;'])
```

### 2- Babel Macro： [babel-plugin-macros](https://github.com/kentcdodds/babel-plugin-macros)

使用上的区别: 引入改为从```styled-components/macro```

```javascript
import styled, { createGlobalStyle } from 'styled-components/macro'
```

### 3- TypeScript Plugin: [typescript-plugin-styled-components](https://github.com/Igorbek/typescript-plugin-styled-components)

### 4- Jest Integration: jest-styled-components

- Snapshot Testing

```javascript
import React from 'react'
import styled from 'styled-components'
import renderer from 'react-test-renderer'
import 'jest-styled-components'

const Button = styled.button`
  color: red;
`

test('it works', () => {
  const tree = renderer.create(<Button />).toJSON()
  expect(tree).toMatchSnapshot()
})
```

测试输出：

```javascript
exports[`it works 1`] = `
.c0 {
  color: green;
}

<button
  className="c0"
/>
`
```

- toHaveStyleRule

```javascript
import React from 'react'
import styled from 'styled-components'
import renderer from 'react-test-renderer'
import 'jest-styled-components'

const Button = styled.button`
  color: red;
  @media (max-width: 640px) {
    &:hover {
      color: green;
    }
  }
`

test('it works', () => {
  const tree = renderer.create(<Button />).toJSON()
  expect(tree).toHaveStyleRule('color', 'red')
  expect(tree).toHaveStyleRule('color', 'green', {
    media: '(max-width: 640px)',
    modifier: ':hover',
  })
})
```

### 5- Stylelint

- 安包： style lint,  [stylelint-processor-styled-components](https://github.com/styled-components/stylelint-processor-styled-components), [stylelint-config-styled-components](https://github.com/styled-components/stylelint-config-styled-components), [stylelint-config-recommended](https://github.com/stylelint/stylelint-config-recommended)

```javascript
(npm install --save-dev \
  stylelint \
  stylelint-processor-styled-components \
  stylelint-config-styled-components \
  stylelint-config-recommended)
```

- Add a .stylelintrc file to the root of your project:

```javascript
{
  "processors": [
    "stylelint-processor-styled-components"
  ],
  "extends": [
    "stylelint-config-recommended",
    "stylelint-config-styled-components"
  ]
}
```

- 启动：在package.json中添加脚本lint:css

```javascript
{
  "scripts": {
    "lint:css":"stylelint './src/**/*.js'"
  }
}
```

-  [stylelint-custom-processor-loader](https://github.com/emilgoldsmith/stylelint-custom-processor-loader)：支持打包stylint

### 6- Styled Theming

```javascript
import React from 'react'
import styled, { ThemeProvider } from 'styled-components'
import theme from 'styled-theming'

const boxBackgroundColor = theme('mode', {
  light: '#fff',
  dark: '#000',
})

const Box = styled.div`
  background-color: ${boxBackgroundColor};
`

export default function App() {
  return (
    <ThemeProvider theme={{ mode: 'light' }}>
      <Box>Hello World</Box>
    </ThemeProvider>
  )
}
```

### 7- API

```ThemeProvider```

- ```them(name, values)```

```javascript
import { ThemeProvider } from 'styled-components'
<ThemeProvider theme={{ mode: "dark", size: "large" }}>
<ThemeProvider theme={{ mode: modes => modes.dark, size: sizes => sizes.large }}>
```

```javascript
// 通过这个函数设置主题
// theme(name, values)
// name should match one of the keys in your <ThemeProvider> theme.
function App() {
  return (
    <ThemeProvider theme={...}>
      {/* rest of your app */}
    </ThemeProvider>
  );
}
// 使用方法
;<ThemeProvider theme={{ whatever: '...' }} />
theme("whatever", {...});
```

```
<ThemeProvider theme={{ mode: "light" }}/>
<ThemeProvider theme={{ mode: "dark" }}/>

theme("mode", {
  light: "...",
  dark: "...",
});
```

The values of this object can be any CSS value.

```javascript
theme("mode", {
  light: "#fff",
  dark: "#000",
});

theme("font", {
  sansSerif: ""Helvetica Neue", Helvetica, Arial, sans-serif",
  serif: "Georgia, Times, "Times New Roman", serif",
  monoSpaced: "Consolas, monaco, monospace",
});
```

These values can also be functions that return CSS values.

```javascript
theme('mode', {
  light: props => props.theme.userProfileAccentColor.light,
  dark: props => props.theme.userProfileAccentColor.dark,
})
```

- ```them.variants(name, prop, themes)```

```javascript
const backgroundColor = theme.variants("mode", "variant", {
  default: { light: "gray", dark: "darkgray" },
  primary: { light: "blue", dark: "darkblue" },
  success: { light: "green", dark: "darkgreen" },
  warning: { light: "orange", dark: "darkorange" },
});

<Button variant="primary"/>
<Button variant="success"/>
<Button variant="warning"/>
```

- 

