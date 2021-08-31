通用首部字段：请求报文和响应报文双方都会使用的首部

- Cache-Control: 能够控制缓存的行为

  ```js
  Cache-Control:private, max-age=0, no-cache
  ```

  no-cahce和no-store的区别

  - no-cache代表不缓存过期的资源，缓存会向源服务器进行有限期确认后处理资源
  - no-store才是真正的不进行缓存

- 表示是否能缓存的指令

  - public
  - private
  - no-cache
  - no-store

- 指定缓存期限和认证的指令

  - s-maxage
  - max-age： 指定资源保存为缓存的最大时间
  - min-fresh： 返回未过指定时间的资源
  - max-stale： 返回缓存资源，无论是否过期
  - only-if-cached： 有缓存才返回，否则504
  - must-revalidate ： 再次验证响应是否有效
  - proxy-revalidate： 必须再次验证资源有效性， 无法连通返回504
  - no-transform： 不能改变 首部主体的媒体类型

  指令同时设置时以哪个为准：

  - s-maxage 和max-age，Expires同时设置: s-maxage 为准
  - max-age和Expires同时设置： Expires为准（HTTP1.0 以Max-age为准）
  - max-stale 和must-revalidate同时设置：must-revalidate

- Pragma

  是HTTP/1.1之前版本的历史遗留字段，只有请求首部有

  ```
  Pragma:no-cache // 要求所有中间服务器不返回缓存的资源
  ```

  兼容的写法：

  ```
  Cache-Control: no-cache
  Pragma: no-cache
  ```

  

