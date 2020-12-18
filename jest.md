安装

```
npm install --save-dev jest
```

使用举例

函数的功能是两数相加

首先创建 `sum.js` 文件：

```javascript
function sum(a, b) {
  return a + b;
}
module.exports = sum;
```

接下来，创建名为 `sum.test.js` 的文件。这个文件包含了实际测试内容：

```javascript
const sum = require('./sum');

test('adds 1 + 2 to equal 3', () => {
  expect(sum(1, 2)).toBe(3);
});
```

将如下代码添加到 `package.json` 中：

```javascript
{
  "scripts": {
    "test": "jest"
  }
}
```

```
npm run test
```

