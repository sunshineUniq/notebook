# react动态修改页面title

原生js修改文档头：

```javascript
document.title = '标题'
```

在react中可以在组件的componentDidMount生命周期中设置

```javascript
document.title = '标题'
```

也可以

```javascript
<Route onEnter={()=>{document.title='标题'}} />
```

或者安装react-helmet，官网的解释是：这个可复用的react组件将管理你在文档头的所以更改。它你可以定制你的页面title，使用起来很简单：

安装：

```bash
npm install react-helmet --save
```

代码： 

```javascript
import React from 'react';
import {Helmet} from 'react-helmet';

class Application extends React.Component {



    render () {
        return (
            <div className="application">
                 <Helmet
        			titleTemplate={`${getAppReleaseKind() === 'a' ? '课堂' : '好老师'}V${getClientVersion()}`}
        			defaultTitle={`${getAppReleaseKind() === 'a' ? '课堂' : '好老师'}V${getClientVersion()}`}
                    meta={[
                      { name: 'description', content: '好老师' },
                    ]}
      			/>
              ...
            </div>
        )
    }
};
```

特性：

1，支持所有有效的头标签，title base meta link script noscript style

2，支持body html title标签的属性

3，支持服务端渲染

4，嵌套组件重写重复的头改变