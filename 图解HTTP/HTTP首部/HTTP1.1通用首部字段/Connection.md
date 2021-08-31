作用：

- 控制不再转发给代理的首部字段

  ```js
  Connection: 不再转发的首部字段名 
  ```

  代理接收到首部后，会将Connection指定的首部字段删除后再转发（被设置成Connection的字段是Hop-by-hop首部）

- 管理持久连接

  关闭持久连接

  ```
  Connection: close
  ```

  HTTP1.1默认是持久连接

  ```
  Connection: Keep-Alive
  ```

  1.1之前的版本默认连接都是非持久连接， 所想想要持久连接，需要给请求设置首部Connection: Keep-Alive

  服务器在响应的时候会加上首部字段Keep-Alive和Connection

  ```
  HTTP/1.1 200 OK
  ...
  Keep-Alive: timeout=10, max=500
  Connection: keep-Alive
  ```

  

  

