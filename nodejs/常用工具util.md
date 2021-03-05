util是一个Nodejs的核心模块，提供常用函数的集合

### util.inherits

```javascript
util.inherits(constructor, superConstructor)
实现对象间原型继承的函数
```

demo

```javascript
var util = require('util')

function Base(params) {
    this.name="base"
    this.base=1991
    this.sayHello = function () {
        console.log('Hello' + this.name);
    }
}

Base.prototype.showName = function () {
    console.log(this.name);
}

function Sub() {
    this.name = 'sub'
}

util.inherits(Sub, Base)

let objBase = new Base()
objBase.showName() // base
objBase.sayHello() // hellobase
console.log("objBase", objBase); //  { name: 'base', base: 1991, sayHello: [Function (anonymous)] }

let objSub = new Sub()
objSub.showName() // sub
objSub.sayHello() // objSub.sayHello is not a function
console.log('objSub', objSub); // { name: 'sub' }
```

结论： sub只继承了原型上的方法和属性

### util.inspect

```javascript
util.inspect(object, [showHidden], [depth], [colors]) //是一个将任意对象转换成字符串的方法，通常用于调试和错误输出
// showHidden---可选参数，如果值是true, 将会输出更多隐藏消息
// depth---表示最大递归的层数，如果对象很复杂，你可以指定层级控制输出信息的多少， 如果不给默认值是2，指定为null,表示完整遍历对象
// colors---值为true, 输出格式将会以ANSI颜色编码，通常用于在终端显示更漂亮的效果

```

demo

```javascript
var util = require('util')

function Person() {
    this.name = 'byvoid'
    this.toString = function () {
        return this.name
    }
}

var obj = new Person()
console.log(util.inspect(obj)); // Person { name: 'byvoid', toString: [Function (anonymous)] }
console.log(util.inspect(obj, true));
/** Person {
  name: 'byvoid',
  toString: <ref *1> [Function (anonymous)] {
    [length]: 0,
    [name]: '',
    [arguments]: null,
    [caller]: null,
    [prototype]: { [constructor]: [Circular *1] }
  }
}
*/
console.log(typeof util.inspect(obj)); // string
```

### 其他

util.isArray()

util.isRegExp()

util.isDate()

util.isError()

util.format()

util.debug()