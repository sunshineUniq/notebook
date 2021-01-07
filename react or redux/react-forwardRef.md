16.3 中增加的函数React.forwardRef： 引用传递

为了解决：是ref拿到子孙组件

我有一个组件Input

使用HOC对他进行了包装， 然后我想拿到Input的值，通过ref 我只能拿到HOCInput，使用forwardRef可以让你直接拿到input

**引用传递**（Ref forwading）是一种通过组件向子组件自动传递 **引用ref** 的技术

使用展示：

```javascript
// 1.基本的使用：通过组件获得input的引用
import React, { Component, createRef, forwardRef } from 'react';

const FocusInput = forwardRef((props, ref) => (
    <input type="text" ref={ref} />
));

class ForwardRef extends Component {
    constructor(props) {
        super(props);
        this.ref = createRef();
    }

    componentDidMount() {
        const { current } = this.ref;
        current.focus();
    }

    render() {
        return (
            <div>
                <p>forward ref</p>
                <FocusInput ref={this.ref} />
            </div>
        );
    }
}
export default ForwardRef;

```

核心方法是React.forwardRef,该方法接受一个有额外ref参数的react组件函数，不调用该方法，普通的组件函数是不会获得该参数的。
 如果子组件中用到了该方法，那么对应的高阶组件中也需要使用React.forwardRef方法

```javascript

import React, { Component, createRef } from 'react';

const FocusInput = React.forwardRef((props, ref) => <input type="text" ref={ref} />);

const bindRef = (WrappedComponent) => {
    const ConvertRef = (props) => {
        const { forwardedRef, ...other } = props;
        console.log(forwardedRef);
        return <WrappedComponent {...other} ref={forwardedRef} />;
    };
    // “ref”是保留字段需要用普通的字段来代替，传递给传入的组件
    return React.forwardRef((props, ref) => {
        console.log(ref);
        return <ConvertRef {...props} forwardedRef={ref} />;
    });
};

const FocusInputWithRef = bindRef(FocusInput);

class ForwardRef extends Component {
    constructor(props) {
        super(props);
        this.ref = createRef();
    }

    componentDidMount() {
        const { current } = this.ref;
        current.focus();
    }

    render() {
        return (
            <div>
                <p>forward ref</p>
                <FocusInputWithRef ref={this.ref} />
            </div>
        );
    }
}
export default ForwardRef;

```

Refs 使用场景

- 处理焦点、文本选择或者媒体的控制
- 触发必要的动画
- 集成第三方 DOM 库