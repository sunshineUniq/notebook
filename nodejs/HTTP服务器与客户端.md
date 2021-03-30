Http服务器与客户端

http模块：封装了一个高效的HTTP服务器（http.server)和一个简易的HTTP客户端(http.request)

### HTTP服务器

```javascript
var http = require('http')
http.createServer((req, res) => {
    res.writeHead(200, {'Content-Type': 'text/html'})
    res.write('<h1>NODE</h1>')
    res.end('<p>hello world</p>')
}).listen(3000)

console.log(' server is listening at port 3000');
```

1、http.Server的事件

提供了以下事件：

>request: 当客户端请求到来时，该事件被触发，提供两个参数req和res, 分别是http.ServerRequest和http.ServerResponse的实例， 表示请求和响应信息
>
>connection: 当TCP连接建立时，该事件被触发，提供一个参数socket, 为net.Socket的实例。connection 事件的粒度要大于request, 因为客户端在Keep-Alive模式下可能会在同一个连接内发送多次请求
>
>close: 当服务器关闭时，该事件被触发。注意不是在用户连接断开时

上面案例的显式的实现方式：

```javascript
const Server = new http.Server()
Server.on('request', function (req, res) {
    res.writeHead(200, { 'Content-Type': 'text/html' })
    res.write('<h1>NODE</h1>')
    res.end('<p>hello world</p>')
})
Server.listen(3000)
console.log('Http server is listening at port 3000');
```

2、http.ServerRequest  

http.ServerRequest是http请求的信息

一般分为两部分：请求头 和 请求体

请求体传输的三个事件：

>data:
>
>请求数据到来时，该事件被触发； 该事件提供一个参数chunk, 表示接收到的数据； 如果该事件没有被监听，那么请求体将会被抛弃；可能会被调用多次
>
>end:
>
>请求体数据传输完成，事件触发；此后将不再有数据进来
>
>close:
>
>用户当前请求结束时，该事件被触发。不同于end, 如果用户强制终止了传输，也还是调用close

3、获取GET请求内容

手动获取地址？后面的参数作为请求参数

Nodejs的url模块的parse函数提供了这个功能

```javascript
var http = require('http')
const util = require('util')
const url = require('url')
const Server = new http.Server()

Server.on('request', function (req, res) {
    res.writeHead(200, {'Content-Type': 'text/plain'});
    res.end(util.inspect(url.parse(req.url, true)))
})

Server.listen(3000)
```

地址栏访问：

http://127.0.0.1:3000/user?name=byvoid&email=byvoid@byvoid.com

页面显示：

![image-20210330151327653](..\img\get请求参数的获取.png)

4、获取POST请求内容

Nodejs默认不会解析请求体，当你需要的时候需要手动来做

```javascript
var http = require('http')
const quireString = require('querystring')
const util = require('util')

http.createServer(function (req, res) {
    const post = ''
    res.on('data', (chunk)=> {
        post += chunk
    })
    res.on('end', () => {
        post = quireString.parse(post)
        res.end(util.inspect(post))
    })
}).listen(3000)
```

注意： 实际应用中不要用上述方式处理post请求

5、http.ServerResponse

有三个重要的成员函数： 响应头， 响应内容， 结束请求

>res.writeHead(statusCode, [headers])
>
>一个请求内最多调用一次，不调用，自动生成一个
>
>res.write(data, [encoding])
>
>想请求的客户端发送响应内容；data是一个Buffer或字符串，要发送的内容
>
>如果data是字符串，需要指定编码方式
>
>在res.end前调用，可以被调用多次
>
>res.end([data], [encoding])
>
>结束响应，告诉客户端所有发送已经完成
>
>必须被调用一次，意义同res.write; 不调用该函数，客户端将永远处于等待状态

### HTTP客户端

http提供了两个函数http.request和http.get， 功能是作为客户端向HTTP服务端发起请求

```javascript
http.request(options, callback)
```

options: 对象

	- host
	- port
	- method
	- path
	- headers

callback: 参数为http.ClienctResponse的实例

http.request的返回值是http.ClientRequest的实例

```javascript
var http = require('http')
var querystring = require('querystring')

var contents = querystring.stringify({
    name: '111',
    email: 'abc@com',
    address: '紫荆里， 江苏'
})

var options = {
    host: 'www.byvoid.com',
    path:'/application/node/post.php',
    method: 'post',
    headers: {
        "Content-Type": 'application/x-www-form-urlencoded',
        'Content-Length': contents.length
    }
}

var req = http.request(options, function (res) {
    res.setEncoding('utf-8');
    res.on('data', function (data) {
        console.log(data);
    })
})

req.write(contents)
req.end()
```

控制台输出

![image-20210330162544873](D:\Users\admin\Desktop\private\notebook\img\httprequest.png)

不要忘了通过req.end结束请求，不然服务端不会受到任何信息

http.get是http.request的简化版，默认method是GET， 且不需要手动req.end

1、http.ClientRequest

http.request或http.get的返回值

表示一个已经产生而且正在进行中的HTTP请求。

2、http.ClientResponse

类似http.ServerRequest

提供了data, end, close

特殊函数：

res.setEncoding([encoding])

res.pause() : 暂停接收数据和发送事件， 方便实现下载功能

res.resume() : 从暂停的状态中恢复









