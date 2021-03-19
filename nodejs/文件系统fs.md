fs模块是文件操作的封装，提供了文件的读取、写入、删除、遍历目录、链接等POSIX文件系统操作

所有模块都有同步和异步方法

- 读取文件

```
fs.readFile(filename, [encoding], [callback(err, data)]) // 异步
```

encoding: 文字的字符编码，不指定data会以Buffer形式表示二进制数据

callback(err, data): err- 读取文件是否有错误发生   data: 文件内容

```javascript
var fs = require('fs')
fs.readFile('./EventEmitter.js',  (err, data) => {
    if(err) {
        console.log(err);
    } else {
        console.log('data', data);
    }
})
```

提示： Nodejs的异步编程接口习惯是以函数的最后一个参数为回调函数，通常一个函数只有一个回调函数。

回调函数的实际参数中第一个是err, 其余参数是其他返回内容。如果没有发生错误， err的值会是null或undefined。如果有错误发生，err通常是Error对象的实例

```
fs.readFileSync(filename, [encoding]) // 同步
```

同步模式读取的内容会通过函数返回值的形式返回， 如果有错误。fs会抛出异常（异步大多没有返回值）

需要配合trycatch捕获异常

```
fs.open(path, flags, [mode], [callback(err, fd)])
```

path是文件的路径， flags可以使下面值

>r: 以读取模式打开文件
>
>r+: 以读写模式打开文件
>
>w: 以写入模式打开文件，如果文件不存在则创建
>
>w+: 以读写模式打开文件，如果文件不存在则创建
>
>a: 以追加模式打开文件，如果文件不存在则创建
>
>a+: 以读取追加模式打开文件， 如果文件不存在则创建

mode： 用于创建文件时给文件指定权限，默认是0666(八进制数）回调函数将会传递一个文件描述符fd（非负整数， 打开文件的记录表索引）

```
fs.read(fd, buffer, offset, length,position, [callback(err, bytesRead, buffer)])
```

fs.read的功能是从指定的文件描述符fd中读取数据并写入buffer指向的缓冲区对象

offset: buffer的写入偏移量

length: 从文件中读取的字节数

position: 文件读取的起始位置，如果position 是null, 则会从当前文件指针的位置读取

callback: 回调函数传递bytesRead和buffer, 分别表示读取的字节数和缓冲区对象

```javascript
var fs = require('fs')

fs.open('./fs.js', 'r', (err, fd) => {
    if(err){
        console.log(err);
        return
    }
    var buf = new Buffer.alloc(8)
    fs.read(fd, buf, 0, 8, null, (err, bytesRead, buffer)=> {
        if(err){
            console.log("22222err", err);
            return
        }
        console.log('bytesRead', bytesRead);
        console.log('buffer', buffer);
    })
})

// bytesRead 8
// buffer <Buffer 76 61 72 20 66 73 20 3d>
```

