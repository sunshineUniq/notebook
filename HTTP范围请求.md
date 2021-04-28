### 一、HTTP 范围请求

Http协议范围允许服务器只发送 HTTP 消息的一部分到客户端

范围请求的使用场景：

- 传送大的媒体文件
- 文件下载的断点续传功能

如果在响应中存在 `Accept-Ranges` 首部（并且它的值不为 “none”），那么表示该服务器支持范围请求。

在一个 Range 首部中，可以一次性请求多个部分, 服务器会以 multipart 文件的形式将其返回

如果服务器返回的是范围响应，需要使用 **206 Partial Content** 状态码, 假如所请求的范围不合法，那么服务器会返回  **416 Range Not Satisfiable** 状态码，表示客户端错误. 服务器允许忽略  Range  首部，从而返回整个文件，状态码用 200 。

<img src=".\img\服务器支持range请求标识.png" style="zoom:50%;" />

#### 1.1 Range语法

```javascript
Range:<unit>=<range-start>-
Range:<unit>=<range-start>-<range-end>
Range:<unit>=<range-start>-<range-end>,<range-start>-<range-end>
Range:<unit>=<range-start>-<range-end>, <range-start>-<range-end>,<range-start>-<range-end>
```

>unit: 范围请求所采用的单位, 通常是bytes
>
><range-starts>: 一个整数，表示在特定单位下，范围的起始值
>
><range-end>: 一个整数， 表示在特定单位下，范围的结束值，**这个值是可选的，如果不存在，表示此范围一直延伸到文档结束。**

实际使用实例：

单一范围

```javascript
curl http://i.imgur.com/z4d4kWk.jpg -i -H "Range: bytes=0-1023"
```

多重范围

```javascript
curl http://www.example.com -i -H "Range: bytes=0-50,100-150"
```

