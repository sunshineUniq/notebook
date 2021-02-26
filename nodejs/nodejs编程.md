// helloworld.js

```javascript
console.log("%s: %d", "hello", 25);
// node 文件
hello: 25
```

##### 运行node程序的基本方法： 

1- ```node script.js```                 2- ```node -e "console.log('hello world')"```

##### 使用node的REPL模式

REPL: Read-eval-print-loop 输入-求值-输出循环

运行无参数的node将会启动一个Javascript的交互shell

![](../img\node-REPL.png)

##### nodejs和PHP架构

![](../img\nodejs与php架构.jpg)

##### 创建http服务器

// app.js

```javascript
var http = require('http');

http.createServer((req, res)=> {
    res.writeHead(200, {"Content-Type": "text/html"})
    res.write('<h1>Node.js</h1>')
    res.end('<p>HELLO WORLD</p>')
}).listen(3000)

console.log('HTTP server is listening at port 3000');
```

node app.js

浏览器访问localhost:3000

![image-20210222112725382](../img\http.png)

小技巧： 使用supervisor

node只有在第一次引用到某部分时才会去解析脚本文件，后面都是直接访问内存，避免重载

开发时我们需要修改后立即看到效果，可以借助supervisor

安装

```
npm i supervisor -g
```

运行

```
supervisor app.js
```

