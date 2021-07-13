#### 请求报文构成： 

​	请求方式 URI 协议版本 

​	请求首部字段

​	内容实体

#### 响应报文构成

​	协议版本 状态码 状态码的原因短语 

​	响应首部字段

​	主体

#### Http是不保存状态的协议（stateless)

http协议自身不具备保存之前发送过的请求或响应的功能

- 引入Cookie技术

#### 告知服务器意图的Http 方法

- GET： 获取资源

- POST： 传输实体主体

- PUT： 传输文件 （http1.1不具有验证机制，不安全）

- HEAD: 获取报文首部（同GET，但不返回报文主体）

- DELETE：删除文件 （http1.1不具有验证机制，不安全）

- OPTIONS：询问支持的方法

  ```javascript
  请求： 
  OPTIONS * HTTP/1.1
  Host: www.hackr.jp
  响应：
  HTTP/1.1 200 OK
  Allow: GET, POST, HEAD, OPTIONS(返回服务器支持的方法)
  ```

- TRACE： 追踪路径 （容易引发XST： Cross-Site Tracing， 跨站追踪攻击）

  ​	Max-Forwards: 2; 没经过一层代理服务器这个值减1，直到为0，服务器返回200 OK

    用来确认连接的过程中发生的一系列操作

  返回的响应包含请求内容

- CONNECT：要求用隧道协议连接代理

​      SSL: Secure Sockets Layer 安全套装层

​     TLS：Transport Layer Security 传输层安全

​	用上面两个对传输内容加密后通过网络隧道传输

#### 持久连接节省通信量

- 持久连接：建立一次TCP 连接后进行多次请求响应的交互
  - 只要任意一端没有明确提出断开连接，一直保存TCP连接状态
- 管线化： 并行发送多个请求

#### 使用Cookie的状态管理

服务端在响应里带上字段Set-Cookie

客户端保存Cookie

下次请求在请求头带上Cookie

服务器端比对Cookie确认客户端身份

