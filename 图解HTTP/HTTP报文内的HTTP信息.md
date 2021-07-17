#### HTTP报文

定义：用于HTTP 协议交互的信息

- 请求报文
- 响应报文

报文首部 + 报文主体

#### 编码提升传输速率

1- http协议的内容编码功能： 压缩内容

常用的内容编码：

- gzip (GNU zip)
- compress (UNIX 系统的标准压缩)
- deflate （zlib)
- identity (不进行编码)

2- 分割发送的分块传输编码（Chunked Transfer Coding)

3- 发送多种数据的多部分对象集合

- multipart/form-data : 表单文件上传时使用
- multipart/byteranges : 状态码206响应报文中包含多个范围的内容时使用

首部字段：content-type， boundary

4- 获取部分内容的范围请求

场景：下载图片失败，需要从之前中断处恢复下载

- 请求头部含有 Range
- 响应首部： 响应码 206 Partial Content ; Content-Range

5- 内容协商返回最合适的内容

场景： 根据浏览器的语言返回不同语言的网页

内容协商的判断基准：语言、字符集、编码方式等

- 请求报文的首部字段时判断基准
  - Accept
  - Accept-Charset
  - Accept-Encoding
  - Accept-Language
  - Content-Language
- 内容协商技术
  - 服务器驱动协商
  - 客户驱动协商
  - 透明协商