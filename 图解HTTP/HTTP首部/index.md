- HTTP 首部传递重要信息： 首部字段内可使用的附加信息较多

- HTTP 首部字段结构

  ```javascript
  首部字段名：字段值  // 字段值可以是多个
  ```

  若HTTP首部字段重复了会如何？

  没有明确的处理规范，不同浏览器处理逻辑不同，有的处理第一次出现的，有的处理最后一次出现的

- 4种HTTP 首部字段类型

  按照用途分：

  - 通用首部字段
  - 请求首部字段
  - 响应首部字段
  - 实体首部字段

- End-to-end 首部 和 Hop-by-hop首部

  HTTP 首部字段将定义成缓存代理和非缓存代理的行为，分成2种类型

  端到端首部： 首部会转发给请求/响应对应的最终接收目标，必须保存在由缓存生成的响应中

  逐跳首部：只对单次转发有效，会因通过缓存或代理而不再转发；HTTP/1.1和之后版本中，如果需要使用hop-by-hop首部，需提供Connection首部字段

  - 逐跳首部字段(8个)
    - Connection
    - Keep-Alive
    - Proxy-Authorization
    - Proxy-Authenticate
    - Trailer
    - TE
    - Transfer-Encoding
    - Upgrade
  - 其他都是端到端首部